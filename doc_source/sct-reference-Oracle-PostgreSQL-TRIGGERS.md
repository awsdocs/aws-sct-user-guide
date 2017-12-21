# Conversion Issues with TRIGGERS<a name="sct-reference-Oracle-PostgreSQL-TRIGGERS"></a>

## Issue 5313: PostgreSQL doesn't support the action\-type clause<a name="sct-reference-5313"></a>

Use another method for this functionality\.

## Issue 5415: PostgreSQL doesn't support system triggers<a name="sct-reference-5415"></a>

Revise your code to replace system triggers with another solution\.

## Issue 5311: PostgreSQL doesn't support system triggers<a name="sct-reference-5311"></a>

Revise your code to replace system triggers with another solution\.

## Issue 5242: PostgreSQL doesn't support COMPOUND TRIGGER<a name="sct-reference-5242"></a>

Create a single trigger for each part of the compound trigger\.

## Issue 5241: PostgreSQL doesn't support the FOLLOWS | PRECEDES clause<a name="sct-reference-5241"></a>

Try using the FOR EACH ROW trigger\.

## Issue 5240: PostgreSQL doesn't support triggers on nested table columns in views<a name="sct-reference-5240"></a>

Revise your code to replace the nested table with another solution\.

## Issue 5238: PostgreSQL doesn't support the REFERENCING clauses<a name="sct-reference-5238"></a>

Modify references to pseudo\-rows to use OLD and NEW instead\.

## Issue 5317: PostgreSQL doesn't support the PARENT referencing clause<a name="sct-reference-5317"></a>

Use another method for this functionality\.

## Issue 5306: Transformation from invalid trigger<a name="sct-reference-5306"></a>

Check the original trigger for errors, and perform the conversion again\.

## Issue 5556: PostgreSQL doesn't support conditional predicates<a name="sct-reference-5556"></a>

Revise your code and try using simple triggers instead\.

## Related Topics<a name="sct-reference-Oracle-PostgreSQL-TRIGGERS-related"></a>

+  [Oracle to PostgreSQL Conversion Reference](sct-reference-Oracle-PostgreSQL.md) 

+  [AWS Schema Conversion Tool Reference](CHAP_SchemaConversionTool.Reference.md) 

+  [What Is the AWS Schema Conversion Tool?](Welcome.md) 