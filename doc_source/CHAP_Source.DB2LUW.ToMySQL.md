# Converting Db2 LUW to Amazon RDS for MySQL or Amazon Aurora MySQL<a name="CHAP_Source.DB2LUW.ToMySQL"></a>

When you convert an IBM Db2 LUW database to RDS for MySQL or Amazon Aurora MySQL, be aware of the following\.

## Privileges for MySQL as a target<a name="CHAP_Source.DB2LUW.ToMySQL.ConfigureTarget"></a>

The privileges required for MySQL as a target are as follows:
+ CREATE ON \*\.\*
+ ALTER ON \*\.\*
+ DROP ON \*\.\*
+ INDEX ON \*\.\*
+ REFERENCES ON \*\.\*
+ SELECT ON \*\.\*
+ CREATE VIEW ON \*\.\*
+ SHOW VIEW ON \*\.\*
+ TRIGGER ON \*\.\*
+ CREATE ROUTINE ON \*\.\*
+ ALTER ROUTINE ON \*\.\*
+ EXECUTE ON \*\.\*
+ SELECT ON mysql\.proc
+ INSERT, UPDATE ON AWS\_DB2\_EXT\.\*
+ INSERT, UPDATE, DELETE ON AWS\_DB2\_EXT\_DATA\.\*
+ CREATE TEMPORARY TABLES ON AWS\_DB2\_EXT\_DATA\.\*

You can use the following code example to create a database user and grant the privileges\.

```
CREATE USER 'user_name' IDENTIFIED BY 'your_password';
GRANT CREATE ON *.* TO 'user_name';
GRANT ALTER ON *.* TO 'user_name';
GRANT DROP ON *.* TO 'user_name';
GRANT INDEX ON *.* TO 'user_name';
GRANT REFERENCES ON *.* TO 'user_name';
GRANT SELECT ON *.* TO 'user_name';
GRANT CREATE VIEW ON *.* TO 'user_name';
GRANT SHOW VIEW ON *.* TO 'user_name';
GRANT TRIGGER ON *.* TO 'user_name';
GRANT CREATE ROUTINE ON *.* TO 'user_name';
GRANT ALTER ROUTINE ON *.* TO 'user_name';
GRANT EXECUTE ON *.* TO 'user_name';
GRANT SELECT ON mysql.proc TO 'user_name';
GRANT INSERT, UPDATE ON AWS_DB2_EXT.* TO 'user_name';
GRANT INSERT, UPDATE, DELETE ON AWS_DB2_EXT_DATA.* TO 'user_name';
GRANT CREATE TEMPORARY TABLES ON AWS_DB2_EXT_DATA.* TO 'user_name';
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

To use Amazon RDS for MySQL or Aurora MySQL as a target, set the `lower_case_table_names` parameter to `1`\. This value means that the MySQL server handles identifiers of such object names as tables, indexes, triggers, and databases as case insensitive\. If you have turned on binary logging in your target instance, then set the `log_bin_trust_function_creators` parameter to `1`\. In this case, you don't need to use the `DETERMINISTIC`, `READS SQL DATA` or `NO SQL` characteristics to create stored functions\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.