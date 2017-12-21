# Conversion Issues with DML<a name="sct-reference-MySQL-PostgreSQL-DML"></a>

## Issue 8829: PostgreSQL doesn't have an analog of clause ON DUPLICATE KEY UPDATE<a name="sct-reference-8829"></a>

Perform a manual conversion\.

## Issue 8830: PostgreSQL doesn't have an option similar to LOW\_PRIORITY for DML statements<a name="sct-reference-8830"></a>

Use the DML statement without this option\.

## Issue 8831: PostgreSQL doesn't have an option similar to IGNORE for DML statements<a name="sct-reference-8831"></a>

Use the DML statement without this option\.

## Issue 8832: PostgreSQL doesn't have an option similar to QUICK for DML statements<a name="sct-reference-8832"></a>

Use the DML statement without this option\.

## Issue 8833: PostgreSQL can't make updates to several tables at the same time<a name="sct-reference-8833"></a>

PostgreSQL doesn't support using an UPDATE statement to update several tables at once, for example `update Account, Customer set Account.AccountBalance = Account.AccountBalance + 100, Customer.SName = 'Sofan Hubert'`\. Perform a manual conversion in this case\.

## Issue 8834: PostgreSQL can't delete from several tables at the same time<a name="sct-reference-8834"></a>

PostgreSQL doesn't support using a DELETE statement to delete several tables at once, for example `delete table1, table3`\. Perform a manual conversion in this case\.

## Issue 8835: PostgreSQL doesn't have an option similar to DELAYED for DML statements<a name="sct-reference-8835"></a>

Use the DML statement without this option\.

## Issue 8836: PostgreSQL doesn't have an option similar to %s for DML statements<a name="sct-reference-8836"></a>

Use the DML statement without this option\.

## Issue 8837: PostgreSQL doesn't support clause STRAIGHT\_JOIN<a name="sct-reference-8837"></a>

Use the DML statement without this option

## Issue 8838: PostgreSQL doesn't support clause SQL\_SMALL\_RESULT<a name="sct-reference-8838"></a>

Use the DML statement without this option

## Issue 8839: PostgreSQL doesn't support clause SQL\_BIG\_RESULT<a name="sct-reference-8839"></a>

Use the DML statement without this option

## Issue 8840: PostgreSQL doesn't support clause SQL\_BUFFER\_RESULT<a name="sct-reference-8840"></a>

Use the DML statement without this option

## Issue 8841: PostgreSQL doesn't support clause SQL\_CACHE<a name="sct-reference-8841"></a>

Use the DML statement without this option

## Issue 8842: PostgreSQL doesn't support clause SQL\_NO\_CACHE<a name="sct-reference-8842"></a>

Use the DML statement without this option

## Issue 8843: PostgreSQL doesn't support clause SQL\_CALC\_FOUND\_ROWS<a name="sct-reference-8843"></a>

Use the DML statement without this option

## Issue 8795: PostgreSQL is case sensitive\. Check the string comparison\.<a name="sct-reference-8795"></a>

Check string comparisons in the WHERE clauses of statements, for example `WHERE [Name] LIKE '%BLOCKED%';`\. All strings used in comparisons must be lowercase\.

## Related Topics<a name="sct-reference-MySQL-PostgreSQL-DML-related"></a>

+  [MySQL to PostgreSQL Conversion Reference](sct-reference-MySQL-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 