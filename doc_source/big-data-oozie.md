# Converting Apache Oozie to AWS Step Functions with the AWS Schema Conversion Tool<a name="big-data-oozie"></a>

To convert Apache Oozie workflows, make sure that you use AWS SCT version 1\.0\.671 or later\. Also, familiarize yourself with the command line interface \(CLI\) of AWS SCT\. For more information, see [AWS SCT CLI Reference](CHAP_Reference.md)\.

**Topics**
+ [Conversion overview](#big-data-oozie-overview)
+ [Step 1: Connect to your source and target services](#big-data-oozie-connect-to-databases)
+ [Step 2: Set up the mapping rules](#big-data-oozie-mapping-rules)
+ [Step 3: Configure parameters](#big-data-oozie-configure-parameters)
+ [Step 4: Create an assessment report](#big-data-oozie-assessment-report)
+ [Step 5: Convert your Apache Oozie workflows to AWS Step Functions with AWS SCT](#big-data-oozie-migrate)
+ [Running your CLI script](#big-data-oozie-run-migration)
+ [Apache Oozie nodes that AWS SCT can convert to AWS Step Functions](#big-data-oozie-supported-nodes)

## Conversion overview<a name="big-data-oozie-overview"></a>

Your Apache Oozie source code includes action nodes, control flow nodes, and job properties\. Action nodes define the jobs, which you run in your Apache Oozie workflow\. When you use Apache Oozie to orchestrate your Apache Hadoop cluster, then an action node includes a Hadoop job\. Control flow nodes provide a mechanism to control the workflow path\. The control flow nodes include such nodes as `start`, `end`, `decision`, `fork`, and `join`\.

AWS SCT converts your source action nodes and control flow nodes to AWS Step Functions\. In AWS Step Functions, you define your workflows in the Amazon States Language \(ASL\)\. AWS SCT uses ASL to define your state machine, which is a collection of states, that can do work, determine which states to transition to next, stop with an error, and so on\. Next, AWS SCT uploads the JSON files with state machines definitions\. Then, AWS SCT can use your AWS Identity and Access Management \(IAM\) role to configure your state machines in AWS Step Functions\. For more information, see [What is AWS Step Functions?](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html) in the *AWS Step Functions Developer Guide*\.

Also, AWS SCT creates an extension pack with AWS Lambda functions which emulate the source functions that AWS Step Functions doesn't support\. For more information, see [Using AWS SCT extension packs](CHAP_ExtensionPack.md)\.

AWS SCT migrates your source job properties to AWS Systems Manager\. To store parameter names and values, AWS SCT uses Parameter Store, a capability of AWS Systems Manager\. For more information, see [What is AWS Systems Manager?](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html) in the *AWS Systems Manager User Guide*\.

You can use AWS SCT to automatically update the values and the names of your parameters\. Because of the architecture differences between Apache Oozie and AWS Step Functions, you might need to configure your parameters\. AWS SCT can find a specified parameter name or value in your source files and replace them with new values\. For more information, see [Step 3: Configure parameters](#big-data-oozie-configure-parameters)\.

The following image shows the architecture diagram of the Apache Oozie conversion to AWS Step Functions\.

![\[The architecture diagram of the Apache Oozie conversion to AWS Step Functions.\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/aws-sct-oozie-conversion-architecture-diagram.png)

To start the conversion, create and run your AWS SCT CLI script\. This script includes the complete set of commands to run the conversion\. You can download and edit a template of the Apache Oozie conversion script\. For more information, see [Getting CLI scenarios](CHAP_Reference.md#CHAP_Reference.Scenario)\.

Make sure that your script includes the following steps\.

## Step 1: Connect to your source and target services<a name="big-data-oozie-connect-to-databases"></a>

To start the conversion of your Apache Oozie cluster, create a new AWS SCT project\. Next, connect to your source and target services\. Make sure that you create and provision your target AWS resources before you start the migration\. For more information, see [Prerequisites for using Apache Oozie as a source](CHAP_Source.Oozie.md#CHAP_Source.Oozie.Prerequisites)\.

In this step, you use the following AWS SCT CLI commands\.
+ `CreateProject` – to create a new AWS SCT project\.
+ `AddSource` – to add your source Apache Oozie files in your AWS SCT project\.
+ `ConnectSource` – to connect to Apache Oozie as a source\.
+ `AddTarget` – to add AWS Step Functions as a migration target in your project\.
+ `ConnectTarget` – to connect to AWS Step Functions\.

For examples of using these AWS SCT CLI commands, see [Using Apache Oozie as a source](CHAP_Source.Oozie.md)\.

When you run the `ConnectSource` or `ConnectTarget` commands, AWS SCT tries to establish the connection to your services\. If the connection attempt fails, then AWS SCT stops running the commands from your CLI script and displays an error message\.

## Step 2: Set up the mapping rules<a name="big-data-oozie-mapping-rules"></a>

After you connect to your source and target services, set up the mapping rules\. A mapping rule defines the migration target for your source Apache Oozie workflows and parameters\. For more information about mapping rules, see [Creating mapping rules in AWS SCT](CHAP_Mapping.md)\.

To define source and target objects for conversion, use the `AddServerMapping` command\. This command uses two parameters: `sourceTreePath` and `targetTreePath`\. The values of these parameters include an explicit path to your source and target objects\. For Apache Oozie to AWS Step Functions conversion, these parameters must start with `ETL`\.

The following code example creates a mapping rule for `OOZIE` and `AWS_STEP_FUNCTIONS` objects\. You added these objects to your AWS SCT project using `AddSource` and `AddTarget` commands in the previous step\.

```
AddServerMapping
    -sourceTreePath: 'ETL.APACHE_OOZIE'
    -targetTreePath: 'ETL.AWS_STEP_FUNCTIONS'
/
```

For more information about the `AddServerMapping` command, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Step 3: Configure parameters<a name="big-data-oozie-configure-parameters"></a>

If your source Apache Oozie workflows use parameters, you might need to change their values after the conversion to AWS Step Functions\. Also, you might need to add new parameters to use with your AWS Step Functions\.

In this step, you use the `AddParameterMapping` and `AddTargetParameter` commands\.

To replace the parameter values in your source files, use the `AddParameterMapping` command\. AWS SCT scans your source files, finds the parameters by name or value, and changes their values\. You can run a single command to scan all your source files\. You define the scope of files to scan using one of the first three parameters from the following list\. This command uses up to six parameters\.
+ `filterName` – the name of the filter for your source objects\. You can create a filter using the `CreateFilter` command\.
+ `treePath` – the explicit path to your source objects\.
+ `namePath` – the explicit path to a specific source object\.
+ `sourceParameterName` – the name of your source parameter\.
+ `sourceValue` – the value of your source parameter\.
+ `targetValue` – the value of your target parameter\.

The following code example replaces all parameters where the value is equal to `c:\oozie\hive.py` with the `s3://bucket-oozie/hive.py` value\.

```
AddParameterMapping
	-treePath: 'ETL.OOZIE.Applications'
	-sourceValue: 'c:\oozie\hive.py'
	-targetValue: 's3://bucket-oozie/hive.py'
/
```

The following code example replaces all parameters where the name is equal to `nameNode` with the `hdfs://ip-111-222-33-44.eu-west-1.compute.internal:8020` value\.

```
AddParameterMapping
    -treePath: 'ETL.OOZIE_SOURCE.Applications'
    -sourceParameter: 'nameNode'
    -targetValue: 'hdfs://ip-111-222-33-44.eu-west-1.compute.internal:8020'
/
```

The following code example replaces all parameters where the name is equal to `nameNode` and the value is equal to `hdfs://ip-55.eu-west-1.compute.internal:8020` with the value from the `targetValue` parameter\.

```
AddParameterMapping
    -treePath: 'ETL.OOZIE_SOURCE.Applications'
    -sourceParameter: 'nameNode'
    -sourceValue: 'hdfs://ip-55-66-77-88.eu-west-1.compute.internal:8020'
    -targetValue: 'hdfs://ip-111-222-33-44.eu-west-1.compute.internal:8020'
/
```

To add a new parameter in your target files in addition to an existing parameter from your source files, use the `AddTargetParameter` command\. This command uses the same set of parameters as the `AddParameterMapping` command\.

The following code example adds the `clusterId` target parameter instead of the `nameNode` parameter\.

```
AddTargetParameter
    -treePath: 'ETL.OOZIE_SOURCE.Applications'
    -sourceParameter: 'nameNode'
    -sourceValue: 'hdfs://ip-55-66-77-88.eu-west-1.compute.internal:8020'
    -targetParameter: 'clusterId'
    -targetValue: '1234567890abcdef0'
/
```

For more information about the `AddServerMapping`, `AddParameterMapping`, `AddTargetParameter`, and `CreateFilter` commands, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Step 4: Create an assessment report<a name="big-data-oozie-assessment-report"></a>

Before you start the conversion, we recommend to create an assessment report\. This report summarizes all of the migration tasks and details the action items that will emerge during the migration\. To make sure that your migration doesn't fail, view this report and address the action items before the migration\. For more information, see [Migration assessment reports](CHAP_AssessmentReport.md)\.

In this step, you use the `CreateReport` command\. This command uses two parameters\. The first parameter describes the source objects for which AWS SCT creates an assessment report\. To do so, use one of the following parameters: `filterName`, `treePath`, or `namePath`\. This parameter is mandatory\. Also, you can add an optional Boolean parameter `forceLoad`\. If you set this parameter to `true`, then AWS SCT automatically loads all child objects for the source object that you specify in the `CreateReport` command\.

The following code example creates an assessment report for the `Applications` node of your source Oozie files\.

```
CreateReport
    -treePath: 'ETL.APACHE_OOZIE.Applications'
/
```

You can then save a copy of the assessment report as a PDF or comma\-separated value \(CSV\) files\. To do so, use the `SaveReportPDF` or `SaveReportCSV` command\.

The `SaveReportPDF` command saves a copy of your assessment report as a PDF file\. This command uses four parameters\. The `file` parameter is mandatory, other parameters are optional\.
+ `file` – the path to the PDF file and its name\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `namePath` – the path that includes only the names of your target objects for which you save a copy of the assessment report\.

The `SaveReportCSV` command saves your assessment report in CSV files\. This command uses four parameters\. The `directory` parameter is mandatory, other parameters are optional\.
+ `directory` – the path to the folder where AWS SCT saves the CSV files\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `namePath` – the path that includes only the names of your target objects for which you save a copy of the assessment report\.

The following code example saves a copy of the assessment report in the `c:\sct\ar.pdf` file\.

```
SaveReportPDF
	-file:'c:\sct\ar.pdf'
/
```

The following code example saves a copy of the assessment report as CSV files in the `c:\sct` folder\.

```
SaveReportCSV
	-file:'c:\sct'
/
```

For more information about the `CreateReport`, `SaveReportPDF` and `SaveReportCSV` commands, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Step 5: Convert your Apache Oozie workflows to AWS Step Functions with AWS SCT<a name="big-data-oozie-migrate"></a>

After you configure your AWS SCT project, convert your source code and apply it to the AWS Cloud\.

In this step, you use the `Convert`, `SaveOnS3`, `ConfigureStateMachine`, and `ApplyToTarget` commands\.

The `Migrate` command migrates your source objects to the target cluster\. This command uses four parameters\. Make sure that you specify the `filter` or `treePath` parameter\. Other parameters are optional\.
+ `filter` – the name of the filter that you created before to define the scope of your source objects to migrate\.
+ `namePath` – the explicit path to a specific source object\.
+ `treePath` – the explicit path to your source database objects for which you save a copy of the assessment report\.
+ `forceLoad` – when set to `true`, AWS SCT automatically loads database metadata trees during migration\. The default value is `false`\.

The following code example converts files from the `Applications` folder in your source Oozie files\.

```
Convert
    -treePath: 'ETL.APACHE_OOZIE.Applications'
/
```

The `SaveOnS3` uploads the state machines definitions to your Amazon S3 bucket\. This command uses the `treePath` parameter\. To run this command, use the target folder with state machines definitions as the value of this parameter\.

The following uploads the `State machine definitions` folder of your `AWS_STEP_FUNCTIONS` target object to the Amazon S3 bucket\. AWS SCT uses the Amazon S3 bucket that you stored in the AWS service profile in the [Prerequisites](CHAP_Source.Oozie.md#CHAP_Source.Oozie.Prerequisites) step\.

```
SaveOnS3
    -treePath: 'ETL.AWS_STEP_FUNCTIONS.State machine definitions'
/
```

The `ConfigureStateMachine` command configures state machines\. This command uses up to six parameters\. Make sure that you define the target scope using one of the first three parameters from the following list\.
+ `filterName` – the name of the filter for your target objects\. You can create a filter using the `CreateFilter` command\.
+ `treePath` – the explicit path to your target objects\.
+ `namePath` – the explicit path to a specific target object\.
+ `iamRole` – the Amazon Resource Name \(ARN\) of the IAM role that provides access to your step machines\. This parameter is required\.

The following code example configures state machines defined in `AWS_STEP_FUNCTIONS` using the *role\_name* IAM role\.

```
ConfigureStateMachine
    -treePath: 'ETL.AWS_STEP_FUNCTIONS.State machine definitions'
    -role: 'arn:aws:iam::555555555555:role/role_name'
/
```

The `ApplyToTarget` command applies your converted code to the target server\. To run this command, use one of the following parameters: `filterName`, `treePath`, or `namePath` to define the target objects to apply\.

The following code example applies the `app_wp` state machine to AWS Step Functions\.

```
ApplyToTarget
    -treePath: 'ETL.AWS_STEP_FUNCTIONS.State machines.app_wp'
/
```

To make sure that your converted code produces the same results as your source code, you can use the AWS SCT extension pack\. This is a set of AWS Lambda functions which emulate your Apache Oozie functions that AWS Step Functions doesn't support\. To install this extension pack, you can use the `CreateLambdaExtPack` command\.

This command uses up to five parameters\. Make sure that you use **Oozie2SF** for `extPackId`\. In this case, AWS SCT creates an extension pack for source Apache Oozie functions\.
+ `extPackId` – the unique identifier for a set of Lambda functions\. This parameter is required\.
+ `tempDirectory` – the path where AWS SCT can store temporary files\. This parameter is required\.
+ `awsProfile` – the name of your AWS profile\.
+ `lambdaExecRoles` – the list of Amazon Resource Names \(ARNs\) of the execution roles to use for Lambda functions\.
+ `createInvokeRoleFlag` – the Boolean flag that indicates whether to create an execution role for AWS Step Functions\.

To install and use the extension pack, make sure that you provide the required permissions\. For more information, see [Permissions for using AWS Lambda functions in the extension pack](CHAP_Source.Oozie.md#CHAP_Source.Oozie.TargetPrerequisites)\.

For more information about the `Convert`, `SaveOnS3`, `ConfigureStateMachine`, `ApplyToTarget`, and `CreateLambdaExtPack` commands, see the [AWS Schema Conversion Tool CLI Reference](https://s3.amazonaws.com/publicsctdownload/AWS+SCT+CLI+Reference.pdf)\.

## Running your CLI script<a name="big-data-oozie-run-migration"></a>

After you finish editing your AWS SCT CLI script, save it as a file with the `.scts` extension\. Now, you can run your script from the `app` folder of your AWS SCT installation path\. To do so, use the following command\.

```
RunSCTBatch.cmd --pathtoscts "C:\script_path\oozie.scts"
```

In the preceding example, replace *script\_path* with the path to your file with the CLI script\. For more information about running CLI scripts in AWS SCT, see [Script mode](CHAP_Reference.md#CHAP_Reference.ScriptMode)\.

## Apache Oozie nodes that AWS SCT can convert to AWS Step Functions<a name="big-data-oozie-supported-nodes"></a>

You can use AWS SCT to convert Apache Oozie action nodes and control flow nodes to AWS Step Functions\.

Supported action nodes include the following:
+ Hive action
+ Hive2 action
+ Spark action
+ MapReduce Streaming action
+ Java action
+ DistCp action
+ Pig action
+ Sqoop action
+ FS action
+ Shell action

Supported control flow nodes include the following:
+ Start action
+ End action
+ Kill action
+ Decision action
+ Fork action
+ Join action