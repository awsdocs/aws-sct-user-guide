# Troubleshooting Issues with the AWS Schema Conversion Tool<a name="CHAP_Troubleshooting"></a>

Following, you can find information about troubleshooting issues with the AWS Schema Conversion Tool \(AWS SCT\)\.

## Cannot load objects from an Oracle source database<a name="CHAP_Troubleshooting.OracleLoad"></a>

When you attempt to load schema from an Oracle database, you might encounter one of the following errors\.

```
Cannot load objects tree.
```

```
ORA-00942: table or view does not exist
```

These errors occur because the user whose ID you used to connect to the Oracle database doesn't have sufficient permissions to read the schema, as required by AWS SCT\. 

You can resolve the issue by granting the user `select_catalog_role` permission and also permission to any dictionary in the database\. These permissions provide the read\-only access to the views and system tables that is required by AWS SCT\. The following example creates a user ID named `min_privs` and grants the user with this ID the minimum permissions required to convert schema from an Oracle source database\. 

```
create user min_privs identified by min_privs;
grant connect to min_privs;
grant select_catalog_role to min_privs;  
grant select any dictionary to min_privs;
```