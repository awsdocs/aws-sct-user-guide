# Conversion Issues with DATA TYPES<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES"></a>

## Issue 7818: PostgreSQL doesn't support arithmetic operations with binary data types<a name="sct-reference-7818"></a>

Perform a manual conversion\.

## Issue 7662: PostgreSQL doesn't support this type\. A manual conversion is required\.<a name="sct-reference-7662"></a>

PostgreSQL doesn't support the geography data type\. To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.

## Issue 7664: PostgreSQL doesn't support this type\. A manual conversion is required\.<a name="sct-reference-7664"></a>

PostgreSQL doesn't support the geometry data type\. To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.

## Issue 7657: PostgreSQL doesn't support this type\. A manual conversion is required\.<a name="sct-reference-7657"></a>

PostgreSQL doesn't support the hierarchyid data type\. To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.

## Issue 7706: PostgreSQL doesn't support this type<a name="sct-reference-7706"></a>

PostgreSQL doesn't support the rowversion data type\. To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type\.

## Issue 7658: PostgreSQL doesn't support this type\. A manual conversion is required\.<a name="sct-reference-7658"></a>

PostgreSQL doesn't support the sql\_variant data type\. To store data of this type in PostgreSQL, use a PostgreSQL\-compatible type or use a composite type\.

## Issue 7659: The scope table\-variables and temporary tables is different\. You must apply manual conversion, if you are using recursion\.<a name="sct-reference-7659"></a>

Perform a manual conversion\.

## Issue 7690: PostgreSQL doesn't support table types<a name="sct-reference-7690"></a>

PostgreSQL doesn’t support table parameters in CREATE PROCEDURE statements, as in the example following\.

```
CREATE TYPE Employee2Client AS TABLE( 
	EmployeeID	int,
	EmployeeName	varchar(160),
	ClientID		int,
	ClientName	varchar(160)
)
go

CREATE PROCEDURE [dbo].[PROC_CREATE_PROC_005]
    @p_E2C	Employee2Client READONLY
AS
BEGIN
	select * from @p_E2C where upper(ClientName) like concat('%', upper('bank'), '%') ;
```

Convert to temporary tables or row variables \(for example, `name table_name%ROWTYPE;`\)\.

## Issue 7816: PostgreSQL doesn't support any methods for data type XML<a name="sct-reference-7816"></a>

Microsoft SQL Server provides methods for the xml data type that you can use to read and manipulate XML data, but PostgreSQL's xml data type does not offer parallel functionality\. Perform a manual conversion to use PostgreSQL XML handling functionality instead\.

## Issue 7817: PostgreSQL doesn't support option \[for xml path\] in the SQL queries<a name="sct-reference-7817"></a>

PostgreSQL doesn't support using the FOR XML clause in PATH mode for DML statements\. Perform a manual conversion to use PostgreSQL XML handling functionality instead\.

## Related Topics<a name="sct-reference-Microsoft-SQL-Server-PostgreSQL-DATATYPES-related"></a>

+  [Microsoft SQL Server to PostgreSQL Conversion Issue Reference](sct-reference-Microsoft-SQL-Server-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 