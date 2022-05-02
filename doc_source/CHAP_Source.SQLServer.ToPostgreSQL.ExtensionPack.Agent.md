# Using an AWS SCT extension pack to emulate SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent"></a>

SQL Server Agent is a Microsoft Windows service that runs SQL Server jobs\. SQL Server Agent runs jobs on a schedule, in response to a specific event, or on demand\. For more information about SQL Server Agent, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/ssms/agent/sql-server-agent?view=sql-server-ver15)\.

PostgreSQL doesn't have an equivalent for SQL Server Agent\. To emulate the SQL Server Agent features, AWS SCT creates an extension pack\. This extension pack uses AWS Lambda and Amazon CloudWatch\. AWS Lambda implements the interface that you use to manage schedules and run jobs\. Amazon CloudWatch maintains the schedule rules\.

AWS Lambda and Amazon CloudWatch use a JSON parameter to interact\. This JSON parameter has the following structure\.

```
{
    "mode": mode,
    "parameters": {
        list of parameters
    },
    "callback": procedure name
}
```

In the preceding example, *`mode`* is the type of the task and `list of parameters` is a set of parameters that depend on the type of the task\. Also, `procedure name` is the name of the procedure that runs after the task is completed\.

AWS SCT uses one Lambda function to control and run jobs\. The CloudWatch rule starts the run of the job and provides the necessary information to start the job\. When the CloudWatch rule triggers, it starts the Lambda function using the parameters from the rule\.

To create a simple job that calls a procedure, use the following format\.

```
{
    "mode": "run_job",
    "parameters": {
        "vendor": "mysql",
        "cmd": "lambda_db.nightly_job"
    }
}
```

To create a job with several steps, use the following format\.

```
{
    "mode": "run_job",
    "parameters": {
        "job_name": "Job1",
        "enabled": "true",
        "start_step_id": 1,
        "notify_level_email": [0|1|2|3],
        "notify_email": email,
        "delete_level": [0|1|2|3],
        "job_callback": "ProcCallBackJob(job_name, code, message)",
        "step_callback": "ProcCallBackStep(job_name, step_id, code, message)"
    },
    "steps": [
        {
            "id":1,
            "cmd": "ProcStep1",
            "cmdexec_success_code": 0,
            "on_success_action": [|2|3|4],
            "on_success_step_id": 1,
            "on_fail_action": 0,
            "on_fail_step_id": 0,
            "retry_attempts": number,
            "retry_interval": number
        },
        {
            "id":2,
            "cmd": "ProcStep2",
            "cmdexec_success_code": 0,
            "on_success_action": [1|2|3|4],
            "on_success_step_id": 0,
            "on_fail_action": 0,
            "on_fail_step_id": 0,
            "retry_attempts": number,
            "retry_interval": number
        },
        ...
]
}
```

To emulate the SQL Server Agent behavior in PostgreSQL, the AWS SCT extension pack also creates the following tables and procedures\.

## Tables that emulate SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.Tables"></a>

To emulate SQL Server Agent, the extension pack uses the following tables:

**sysjobs**  
Stores the information about the jobs\.

**sysjobsteps**  
Stores the information about the steps of a job\.

**sysschedules**  
Stores the information about the job schedules\.

**sysjobschedules**  
Stores the schedule information for individual jobs\. 

**sysjobhistory**  
Stores the information about the runs of scheduled jobs\.

## Procedures that emulate SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.Procedures"></a>

To emulate SQL Server Agent, the extension pack uses the following procedures:

**sp\_add\_job**  
Adds a new job\.

**sp\_add\_jobstep**  
Adds a step to a job\.

**sp\_add\_schedule**  
Creates a new schedule rule in Amazon CloudWatch\. You can use this schedule with any number of jobs\.

**sp\_attach\_schedule**  
Sets a schedule for the selected job\.

**sp\_add\_jobschedule**  
Creates a schedule rule for a job in Amazon CloudWatch and sets the target for this rule\.

**sp\_update\_job**  
Updates the attributes of the previously created job\.

**sp\_update\_jobstep**  
Updates the attributes of the step in a job\.

**sp\_update\_schedule**  
Updates the attributes of a schedule rule in Amazon CloudWatch\.

**sp\_update\_jobschedule**  
Updates the attributes of the schedule for the specified job\.

**sp\_delete\_job**  
Deletes a job\.

**sp\_delete\_jobstep**  
Deletes a job step from a job\.

**sp\_delete\_schedule**  
Deletes a schedule\.

**sp\_delete\_jobschedule**  
Deletes the schedule rule for the specified job from Amazon CloudWatch\.

**sp\_detach\_schedule**  
Removes an association between a schedule and a job\.

**get\_jobs, update\_job**  
Internal procedures that interact with AWS Elastic Beanstalk\.

**sp\_verify\_job\_date, sp\_verify\_job\_time, sp\_verify\_job, sp\_verify\_jobstep, sp\_verify\_schedule, sp\_verify\_job\_identifiers, sp\_verify\_schedule\_identifiers**  
Internal procedures that check settings\.

## Syntax for procedures that emulate SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.Syntax"></a>

The `aws_sqlserver_ext.sp_add_job` procedure in the extension pack emulates the `msdb.dbo.sp_add_job` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql?view=sql-server-ver15)\. 

```
par_job_name varchar,
par_enabled smallint = 1,
par_description varchar = NULL::character varying,
par_start_step_id integer = 1,
par_category_name varchar = NULL::character varying,
par_category_id integer = NULL::integer,
par_owner_login_name varchar = NULL::character varying,
par_notify_level_eventlog integer = 2,
par_notify_level_email integer = 0,
par_notify_level_netsend integer = 0,
par_notify_level_page integer = 0,
par_notify_email_operator_name varchar = NULL::character varying,
par_notify_netsend_operator_name varchar = NULL::character varying,
par_notify_page_operator_name varchar = NULL::character varying,
par_delete_level integer = 0,
inout par_job_id integer = NULL::integer,
par_originating_server varchar = NULL::character varying,
out returncode integer
```

The `aws_sqlserver_ext.sp_add_jobstep` procedure in the extension pack emulates the `msdb.dbo.sp_add_jobstep` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_step_id integer = NULL::integer,
par_step_name varchar = NULL::character varying,
par_subsystem varchar = 'TSQL'::bpchar,
par_command text = NULL::text,
par_additional_parameters text = NULL::text,
par_cmdexec_success_code integer = 0,
par_on_success_action smallint = 1,
par_on_success_step_id integer = 0,
par_on_fail_action smallint = 2,
par_on_fail_step_id integer = 0,
par_server varchar = NULL::character varying,
par_database_name varchar = NULL::character varying,
par_database_user_name varchar = NULL::character varying,
par_retry_attempts integer = 0,
par_retry_interval integer = 0,
par_os_run_priority integer = 0,
par_output_file_name varchar = NULL::character varying,
par_flags integer = 0,
par_proxy_id integer = NULL::integer,
par_proxy_name varchar = NULL::character varying,
inout par_step_uid char = NULL::bpchar,
out returncode integer
```

The `aws_sqlserver_ext.sp_add_schedule` procedure in the extension pack emulates the `msdb.dbo.sp_add_schedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql?view=sql-server-ver15)\. 

```
par_schedule_name varchar,
par_enabled smallint = 1,
par_freq_type integer = 0,
par_freq_interval integer = 0,
par_freq_subday_type integer = 0,
par_freq_subday_interval integer = 0,
par_freq_relative_interval integer = 0,
par_freq_recurrence_factor integer = 0,
par_active_start_date integer = NULL::integer,
par_active_end_date integer = 99991231,
par_active_start_time integer = 0,
par_active_end_time integer = 235959,
par_owner_login_name varchar = NULL::character varying,
*inout par_schedule_uid char = NULL::bpchar,*
inout par_schedule_id integer = NULL::integer,
par_originating_server varchar = NULL::character varying,
out returncode integer
```

The `aws_sqlserver_ext.sp_attach_schedule` procedure in the extension pack emulates the `msdb.dbo.sp_attach_schedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_schedule_id integer = NULL::integer,
par_schedule_name varchar = NULL::character varying,
par_automatic_post smallint = 1,
out returncode integer
```

The `aws_sqlserver_ext.sp_add_jobschedule` procedure in the extension pack emulates the `msdb.dbo.sp_add_jobschedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_name varchar = NULL::character varying,
par_enabled smallint = 1,
par_freq_type integer = 1,
par_freq_interval integer = 0,
par_freq_subday_type integer = 0,
par_freq_subday_interval integer = 0,
par_freq_relative_interval integer = 0,
par_freq_recurrence_factor integer = 0,
par_active_start_date integer = NULL::integer,
par_active_end_date integer = 99991231,
par_active_start_time integer = 0,
par_active_end_time integer = 235959,
inout par_schedule_id integer = NULL::integer,
par_automatic_post smallint = 1,
inout par_schedule_uid char = NULL::bpchar,
out returncode integer
```

The `aws_sqlserver_ext.sp_delete_job` procedure in the extension pack emulates the `msdb.dbo.sp_delete_job` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_originating_server varchar = NULL::character varying,
par_delete_history smallint = 1,
par_delete_unused_schedule smallint = 1,
out returncode integer
```

The `aws_sqlserver_ext.sp_delete_jobstep` procedure in the extension pack emulates the `msdb.dbo.sp_delete_jobstep` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_step_id integer = NULL::integer,
out returncode integer
```

The `aws_sqlserver_ext.sp_delete_jobschedule` procedure in the extension pack emulates the `msdb.dbo.sp_delete_jobschedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-delete-jobschedule-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_name varchar = NULL::character varying,
par_keep_schedule integer = 0,
par_automatic_post smallint = 1,
out returncode integer
```

The `aws_sqlserver_ext.sp_delete_schedule` procedure in the extension pack emulates the `msdb.dbo.sp_delete_schedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql?view=sql-server-ver15)\. 

```
par_schedule_id integer = NULL::integer,
par_schedule_name varchar = NULL::character varying,
par_force_delete smallint = 0,
par_automatic_post smallint = 1,
out returncode integer
```

The `aws_sqlserver_ext.sp_detach_schedule` procedure in the extension pack emulates the `msdb.dbo.sp_detach_schedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer,
par_job_name varchar = NULL::character varying,
par_schedule_id integer = NULL::integer,
par_schedule_name varchar = NULL::character varying,
par_delete_unused_schedule smallint = 0,
par_automatic_post smallint = 1,
out returncode integer
```

The `aws_sqlserver_ext.sp_update_job` procedure in the extension pack emulates the `msdb.dbo.sp_update_job` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer
par_job_name varchar = NULL::character varying
par_new_name varchar = NULL::character varying
par_enabled smallint = NULL::smallint
par_description varchar = NULL::character varying
par_start_step_id integer = NULL::integer
par_category_name varchar = NULL::character varying
par_owner_login_name varchar = NULL::character varying
par_notify_level_eventlog integer = NULL::integer
par_notify_level_email integer = NULL::integer
par_notify_level_netsend integer = NULL::integer
par_notify_level_page integer = NULL::integer
par_notify_email_operator_name varchar = NULL::character varying
par_notify_netsend_operator_name varchar = NULL::character varying
par_notify_page_operator_name varchar = NULL::character varying
par_delete_level integer = NULL::integer
par_automatic_post smallint = 1
out returncode integer
```

The `aws_sqlserver_ext.sp_update_jobschedule` procedure in the extension pack emulates the `msdb.dbo.sp_update_jobschedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-update-jobschedule-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer
par_job_name varchar = NULL::character varying
par_name varchar = NULL::character varying
par_new_name varchar = NULL::character varying
par_enabled smallint = NULL::smallint
par_freq_type integer = NULL::integer
par_freq_interval integer = NULL::integer
par_freq_subday_type integer = NULL::integer
par_freq_subday_interval integer = NULL::integer
par_freq_relative_interval integer = NULL::integer
par_freq_recurrence_factor integer = NULL::integer
par_active_start_date integer = NULL::integer
par_active_end_date integer = NULL::integer
par_active_start_time integer = NULL::integer
                par_active_end_time integer = NULL::integer
par_automatic_post smallint = 1
out returncode integer
```

The `aws_sqlserver_ext.sp_update_jobstep` procedure in the extension pack emulates the `msdb.dbo.sp_update_jobstep` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql?view=sql-server-ver15)\. 

```
par_job_id integer = NULL::integer
par_job_name varchar = NULL::character varying
par_step_id integer = NULL::integer
par_step_name varchar = NULL::character varying
par_subsystem varchar = NULL::character varying
par_command text = NULL::text
par_additional_parameters text = NULL::text
par_cmdexec_success_code integer = NULL::integer
par_on_success_action smallint = NULL::smallint
par_on_success_step_id integer = NULL::integer
par_on_fail_action smallint = NULL::smallint
par_on_fail_step_id integer = NULL::integer
par_server varchar = NULL::character varying
par_database_name varchar = NULL::character varying
par_database_user_name varchar = NULL::character varying
par_retry_attempts integer = NULL::integer
par_retry_interval integer = NULL::integer
par_os_run_priority integer = NULL::integer
par_output_file_name varchar = NULL::character varying
par_flags integer = NULL::integer
par_proxy_id integer = NULL::integer
par_proxy_name varchar = NULL::character varying
out returncode integer
```

The `aws_sqlserver_ext.sp_update_schedule` procedure in the extension pack emulates the `msdb.dbo.sp_update_schedule` procedure\. For more information about the source SQL Server Agent procedure, see [Microsoft technical documentation](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql?view=sql-server-ver15)\. 

```
par_schedule_id integer = NULL::integer
par_name varchar = NULL::character varying
par_new_name varchar = NULL::character varying
par_enabled smallint = NULL::smallint
par_freq_type integer = NULL::integer
par_freq_interval integer = NULL::integer
par_freq_subday_type integer = NULL::integer
par_freq_subday_interval integer = NULL::integer
par_freq_relative_interval integer = NULL::integer
par_freq_recurrence_factor integer = NULL::integer
par_active_start_date integer = NULL::integer
par_active_end_date integer = NULL::integer
par_active_start_time integer = NULL::integer
par_active_end_time integer = NULL::integer
par_owner_login_name varchar = NULL::character varying
par_automatic_post smallint = 1
out returncode integer
```

## Examples for using procedures that emulate SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.Examples"></a>

To add a new job, use the `aws_sqlserver_ext.sp_add_job` procedure as shown following\.

```
SELECT * FROM aws_sqlserver_ext.sp_add_job (
    par_job_name := 'test_job',
    par_enabled := 1::smallint,
    par_start_step_id := 1::integer,
    par_category_name := '[Uncategorized (Local)]',
    par_owner_login_name := 'sa');
```

To add a new job step, use the `aws_sqlserver_ext.sp_add_jobstep` procedure as shown following\.

```
SELECT * FROM aws_sqlserver_ext.sp_add_jobstep (
    par_job_name := 'test_job',
    par_step_id := 1::smallint,
    par_step_name := 'test_job_step1',
    par_subsystem := 'TSQL',
    par_command := 'EXECUTE [dbo].[PROC_TEST_JOB_STEP1];',
    par_server := NULL,
    par_database_name := 'GOLD_TEST_SS');
```

To add a simple schedule, use the `aws_sqlserver_ext.sp_add_schedule` procedure as shown following\.

```
SELECT * FROM aws_sqlserver_ext.sp_add_schedule(
    par_schedule_name := 'RunOnce',
    par_freq_type := 1,
    par_active_start_time := 233000);
```

To set a schedule for a job, use the `aws_sqlserver_ext.sp_attach_schedule` procedure as shown following\.

```
SELECT * FROM aws_sqlserver_ext.sp_attach_schedule (
    par_job_name := 'test_job',
    par_schedule_name := 'NightlyJobs');
```

To create a schedule for a job, use the `aws_sqlserver_ext.sp_add_jobschedule` procedure as shown following\.

```
SELECT * FROM aws_sqlserver_ext.sp_add_jobschedule (
    par_job_name := 'test_job2',
    par_name := 'test_schedule2',
    par_enabled := 1::smallint,
    par_freq_type := 4,
    par_freq_interval := 1,
    par_freq_subday_type := 4,
    par_freq_subday_interval := 1,
    par_freq_relative_interval := 0,
    par_freq_recurrence_factor := 0,
    par_active_start_date := 20100801,
    par_active_end_date := 99991231,
    par_active_start_time := 0,
    par_active_end_time := 0);
```

## Use case examples for emulating SQL Server Agent in PostgreSQL<a name="CHAP_Source.SQLServer.ToPostgreSQL.ExtensionPack.Agent.UseCases"></a>

If your source database code uses SQL Server Agent to run jobs, you can use the SQL Server to PostgreSQL extension pack for AWS SCT to convert this code to PostgreSQL\. The extension pack uses AWS Lambda functions to emulate the behavior of SQL Server Agent\.

You can create a new AWS Lambda function or register an existing function\.

**To create a new AWS Lambda function**

1. In the AWS SCT, in the target database tree, open the context \(right\-click\) menu, choose **Apply extension pack for**, and then choose **PostgreSQL**\. 

   The extension pack wizard appears\. 

1. On the **SQL Server Agent emulation service** tab, do the following: 
   + Choose **Create an AWS Lambda function**\.
   + For **Database login**, enter the name of the target database user\.
   + For **Database password**, enter the password for the user name that you entered on the preceding step\.
   + For **Python library folder**, enter the path to your Python library folder\.
   + Choose **Create AWS Lambda function**, and then choose **Next**\.

**To register an AWS Lambda function that you deployed earlier**
+ Run the following script on your target database\.

  ```
  SELECT
      FROM aws_sqlserver_ext.set_service_setting(
          p_service := 'JOB', 
          p_setting := 'LAMBDA_ARN', 
          p_value := ARN)
  ```

  In the preceding example, *`ARN`* is the Amazon Resource Name \(ARN\) of the deployed AWS Lambda function\.

The following example creates a simple task that consists of one step\. Every five minutes, this task runs the previously created `job_example` function\. This function inserts records into the `job_example_table` table\.

**To create this simple task**

1. Create a job using the `aws_sqlserver_ext.sp_add_job` function as shown following\.

   ```
   SELECT
       FROM aws_sqlserver_ext.sp_add_job (
           par_job_name := 'test_simple_job');
   ```

1. Create a job step using the `aws_sqlserver_ext.sp_add_jobstep` function as shown following\.

   ```
   SELECT
       FROM aws_sqlserver_ext.sp_add_jobstep (
           par_job_name := 'test_simple_job', 
           par_step_name := 'test_simple_job_step1', 
           par_command := 'PERFORM job_simple_example;');
   ```

   The job step specifies what the function does\.

1. Create a scheduler for the job using the `aws_sqlserver_ext.sp_add_jobschedule` function as shown following\.

   ```
   SELECT
       FROM aws_sqlserver_ext.sp_add_jobschedule (
           par_job_name := 'test_simple_job', 
           par_name := 'test_schedule', 
           par_freq_type := 4, /* Daily */
           par_freq_interval := 1, /* frequency_interval is unused */
           par_freq_subday_type := 4, /* Minutes */
           par_freq_subday_interval := 5 /* 5 minutes */);
   ```

   The job step specifies what the function does\.

To delete this job, use the `aws_sqlserver_ext.sp_delete_job` function as shown following\.

```
PERFORM aws_sqlserver_ext.sp_delete_job(
    par_job_name := 'PeriodicJob1'::character varying,
    par_delete_history := 1::smallint,
    par_delete_unused_schedule := 1::smallint);
```