# Conversion Issues with BUILT\-IN SQL FUNCTIONS<a name="sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS"></a>

## Issue 5584: The function %s depends on the time zone setting<a name="sct-reference-5584"></a>

Review the transformed code, and set the time zone manually if necessary\.

## Issue 5340: PostgreSQL doesn't support the %s function<a name="sct-reference-5340"></a>

You have SQL code that uses an Oracle function that PostgreSQL doesn't support\. Re\-write the code to either use an alternative function or create a user\-defined function instead\. Some of the functions that are not supported are as follows:

+ NANVL

+ NLS\_LOWER

+ NLS\_UPPER

+ SYS\_CONTEXT

## Issue 5271: The Oracle GREATEST function and PostgreSQL GREATEST function might give different results<a name="sct-reference-5271"></a>

Review your transformed code and modify it to change the argument's type if necessary\.

## Issue 5272: The Oracle LEAST function and PostgreSQL LEAST function might give different results<a name="sct-reference-5272"></a>

Review your transformed code and modify it to change the argument's type if necessary\.

## Issue 5579: The second parameter of %s function can be processed incorrectly<a name="sct-reference-5579"></a>

Review your transformed code and modify it if necessary\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-BUILT-INSQLFUNCTIONS-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 