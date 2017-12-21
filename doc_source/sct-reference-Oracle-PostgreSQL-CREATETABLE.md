# Conversion Issues with CREATE TABLE<a name="sct-reference-Oracle-PostgreSQL-CREATETABLE"></a>

## Issue 5212: PostgreSQL doesn't have a data type BFILE<a name="sct-reference-5212"></a>

Either store a named file with the data and create a routine that gets that file from the file system, or store the data blob inside your database\.

## Issue 5201: PostgreSQL doesn't support all partition types<a name="sct-reference-5201"></a>

Perform a manual conversion for the partition types that aren't supported\.

## Issue 5199: PostgreSQL doesn't support CLUSTERED TABLE<a name="sct-reference-5199"></a>

Try using a table with triggers instead\.

## Issue 5200: PostgreSQL doesn't support EXTERNAL TABLES<a name="sct-reference-5200"></a>

Try moving the data from the external data source to a regular database table\.

## Issue 5198: PostgreSQL doesn't support GLOBAL TEMPORARY TABLE<a name="sct-reference-5198"></a>

Use of the GLOBAL and LOCAL keywords is deprecated in PostgreSQL\. Modify your code to create a temporary table without using these keywords\.

## Issue 5196: PostgreSQL doesn't support OBJECT TABLE<a name="sct-reference-5196"></a>

Revise your code to remove references to tables that are based on an OBJECT type, as shown in the following example:

```
CREATE TYPE department_typ AS OBJECT
   ( d_name     VARCHAR2(100),
     d_address  VARCHAR2(200) );
/
  CREATE TABLE departments_obj_t OF department_typ;
```

## Issue 5581: PostgreSQL doesn't support index\-organized table<a name="sct-reference-5581"></a>

Revise your architecture with a custom solution for the table type\. A typical approach is using a simple table instead in PostgreSQL\.

## Issue 5348: PostgreSQL doesn't support NESTED TABLES<a name="sct-reference-5348"></a>

Revise your code to avoid NESTED TABLE\.

## Issue 5550: PostgreSQL doesn't have a data type ROWID<a name="sct-reference-5550"></a>

Review your transformed code and modify it if necessary to use a different data type\.

## Issue 5554: PostgreSQL doesn't support virtual columns<a name="sct-reference-5554"></a>

Emulate the virtual column by using a trigger instead\. For example, you could modify the following Oracle table:

```
CREATE TABLE employees2 (
  id          NUMBER,
  first_name  VARCHAR2(10),
  last_name   VARCHAR2(10),
  salary      NUMBER(9,2),
  comm1       NUMBER(3),
  comm2       NUMBER(3),
  salary1     AS (ROUND(salary*(1+comm1/100),2)),
  salary2     NUMBER GENERATED ALWAYS AS (ROUND(salary*(1+comm2/100),2)) VIRTUAL,
  CONSTRAINT employees_pk PRIMARY KEY (id)
);
```

To the following PostgreSQL statements:

```
CREATE TABLE IF NOT EXISTS TEST_ORA_PG.employees2 (
  id          DOUBLE PRECISION NOT NULL,
  first_name  character varying(10),
  last_name   character varying(10),
  salary      NUMERIC(9,2),
  comm1       NUMERIC(3,0),
  comm2       NUMERIC(3,0),
  salary1     DOUBLE PRECISION,
  salary2     DOUBLE PRECISION
); 


ALTER TABLE TEST_ORA_PG.EMPLOYEES2
ADD CONSTRAINT EMPLOYEES_PK PRIMARY KEY (ID);


CREATE OR REPLACE FUNCTION TEST_ORA_PG.f_trigger_vc$employees2 ()
RETURNS trigger
AS 
$BODY$ 
BEGIN 
     new.salary1 := ROUND(new.salary*(1+new.comm1/100),2);
     new.salary2 := ROUND(new.salary*(1+new.comm2/100),2);
return NEW;
END; 
$BODY$
 LANGUAGE  plpgsql;
 
CREATE TRIGGER trigger_vc$employees2
before insert  or update on TEST_ORA_PG.employees2
for each row
EXECUTE PROCEDURE TEST_ORA_PG.f_trigger_vc$employees2();
```

## Issue 5213: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision<a name="sct-reference-5213"></a>

Review your transformed code and modify it if necessary to avoid a loss of accuracy\.

## Issue 5552: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision<a name="sct-reference-5552"></a>

Review your transformed code and modify it if necessary to avoid a loss of accuracy\.

## Issue 5553: PostgreSQL expands fractional seconds support for TIME, DATETIME, and TIMESTAMP values, with up to microseconds \(6 digits\) of precision<a name="sct-reference-5553"></a>

Review your transformed code and modify it if necessary to avoid a loss of accuracy\.

## Issue 5551: PostgreSQL doesn't have a data type UROWID<a name="sct-reference-5551"></a>

Review your transformed code and modify it if necessary to use a different data type\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-CREATETABLE-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 