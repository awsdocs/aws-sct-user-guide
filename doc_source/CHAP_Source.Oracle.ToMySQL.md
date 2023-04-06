# Converting Oracle to Amazon RDS for MySQL or Amazon Aurora MySQL<a name="CHAP_Source.Oracle.ToMySQL"></a>

To emulate Oracle database functions in your converted MySQL code, use the Oracle to MySQL extension pack in AWS SCT\. For more information about extension packs, see [Using AWS SCT extension packs](CHAP_ExtensionPack.md)\. 

**Topics**
+ [Privileges for MySQL as a target database](#CHAP_Source.Oracle.ToMySQL.ConfigureTarget)
+ [Oracle to MySQL conversion settings](#CHAP_Source.Oracle.ToMySQL.ConversionSettings)
+ [Migration considerations](#CHAP_Source.Oracle.ToMySQL.MigrationConsiderations)
+ [Converting the WITH statement in Oracle to RDS for MySQL or Amazon Aurora MySQL](#CHAP_Source.Oracle.ToMySQL.With)

## Privileges for MySQL as a target database<a name="CHAP_Source.Oracle.ToMySQL.ConfigureTarget"></a>

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
+ CREATE TEMPORARY TABLES ON \*\.\*
+ AWS\_LAMBDA\_ACCESS
+ INSERT, UPDATE ON AWS\_ORACLE\_EXT\.\*
+ INSERT, UPDATE, DELETE ON AWS\_ORACLE\_EXT\_DATA\.\*

If you use a MySQL database version 5\.7 or lower as a target, then grant the INVOKE LAMBDA \*\.\* permission instead of AWS\_LAMBDA\_ACCESS\. For MySQL databases version 8\.0 and higher, grant the AWS\_LAMBDA\_ACCESS permission\.

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
GRANT CREATE TEMPORARY TABLES ON *.* TO 'user_name';
GRANT AWS_LAMBDA_ACCESS TO 'user_name';
GRANT INSERT, UPDATE ON AWS_ORACLE_EXT.* TO 'user_name';
GRANT INSERT, UPDATE, DELETE ON AWS_ORACLE_EXT_DATA.* TO 'user_name';
```

In the preceding example, replace *user\_name* with the name of your user\. Then, replace *your\_password* with a secure password\.

If you use a MySQL database version 5\.7 or lower as a target, then use `GRANT INVOKE LAMBDA ON *.* TO 'user_name'` instead of `GRANT AWS_LAMBDA_ACCESS TO 'user_name'`\.

To use Amazon RDS for MySQL or Aurora MySQL as a target, set the `lower_case_table_names` parameter to `1`\. This value means that the MySQL server handles identifiers of such object names as tables, indexes, triggers, and databases as case insensitive\. If you have turned on binary logging in your target instance, then set the `log_bin_trust_function_creators` parameter to `1`\. In this case, you don't need to use the `DETERMINISTIC`, `READS SQL DATA` or `NO SQL` characteristics to create stored functions\. To configure these parameters, create a new DB parameter group or modify an existing DB parameter group\.

## Oracle to MySQL conversion settings<a name="CHAP_Source.Oracle.ToMySQL.ConversionSettings"></a>

To edit Oracle to MySQL conversion settings, choose **Settings** in AWS SCT, and then choose **Conversion settings**\. From the upper list, choose **Oracle**, and then choose **Oracle – MySQL**\. AWS SCT displays all available settings for Oracle to MySQL conversion\.

Oracle to MySQL conversion settings in AWS SCT include options for the following:
+ To limit the number of comments with action items in the converted code\.

  For **Add comments in the converted code for the action items of selected severity and higher**, choose the severity of action items\. AWS SCT adds comments in the converted code for action items of the selected severity and higher\.

  For example, to minimize the number of comments in your converted code, choose **Errors only**\. To include comments for all action items in your converted code, choose **All messages**\.
+ To address that your source Oracle database can use the `ROWID` pseudocolumn but MySQL doesn't support similar functionality\. AWS SCT can emulate the `ROWID` pseudocolumn in the converted code\. To do so, choose **Generate as identity** for **Generate row ID?**\.

  If your source Oracle code doesn't use the `ROWID` pseudocolumn, choose **Don't generate** for **Generate row ID?** In this case, the converted code works faster\.
+ To work with your source Oracle code when it includes the `TO_CHAR`, `TO_DATE`, and `TO_NUMBER` functions with parameters that MySQL doesn't support\. By default, AWS SCT emulates the usage of these parameters in the converted code\.

  When your source Oracle code includes only parameters that PostgreSQL supports, you can use native MySQL `TO_CHAR`, `TO_DATE`, and `TO_NUMBER` functions\. In this case, the converted code works faster\. To include only these parameters, select the following values:
  + **Function TO\_CHAR\(\) does not use Oracle specific formatting strings**
  + **Function TO\_DATE\(\) does not use Oracle specific formatting strings**
  + **Function TO\_NUMBER\(\) does not use Oracle specific formatting strings**
+ To addess whether your database and applications run in different time zones\. By default, AWS SCT emulates time zones in the converted code\. However, you don't need this emulation when your database and applications use the same time zone\. In this case, select **Time zone on the client side matches the time zone on server**\.

## Migration considerations<a name="CHAP_Source.Oracle.ToMySQL.MigrationConsiderations"></a>

When you convert Oracle to RDS for MySQL or Aurora MySQL, to change the order that statements run in, you can use a `GOTO` statement and a label\. Any PL/SQL statements that follow a `GOTO` statement are skipped, and processing continues at the label\. You can use `GOTO` statements and labels anywhere within a procedure, batch, or statement block\. You can also next GOTO statements\.

MySQL doesn't use `GOTO` statements\. When AWS SCT converts code that contains a `GOTO` statement, it converts the statement to use a `BEGIN…END` or `LOOP…END LOOP` statement\. 

You can find examples of how AWS SCT converts `GOTO` statements in the table following\.


| Oracle statement | MySQL statement | 
| --- | --- | 
|  <pre>BEGIN<br />   ....<br />   statement1;<br />   ....<br />   GOTO label1;<br />   statement2;<br />   ....<br />   label1:<br />   Statement3;<br />   ....<br />END<br /></pre>  |  <pre>BEGIN<br /> label1:<br /> BEGIN<br />   ....<br />   statement1;<br />   ....<br />   LEAVE label1;<br />   statement2;<br />   ....<br /> END;<br />   Statement3;<br />   ....<br />END<br /></pre>  | 
|  <pre>BEGIN<br />   ....<br />   statement1;<br />   ....<br />   label1:<br />   statement2;<br />   ....<br />   GOTO label1;<br />   statement3;<br />   ....<br />   statement4;<br />   ....<br />END<br /></pre>  |  <pre>BEGIN<br />   ....<br />   statement1;<br />   ....<br />   label1:<br />   LOOP<br />    statement2;<br />    ....<br />    ITERATE label1;<br />    LEAVE label1;<br />   END LOOP; <br />    statement3;<br />    ....<br />    statement4;<br />    ....<br />END<br /></pre>  | 
|  <pre>BEGIN<br />   ....<br />   statement1;<br />   ....<br />   label1:<br />   statement2;<br />   ....<br />   statement3;<br />   ....<br />   statement4;<br />   ....<br />END<br /></pre>  |  <pre>BEGIN<br />   ....<br />   statement1;<br />   ....<br />   label1:<br />   BEGIN<br />    statement2;<br />    ....    <br />    statement3;<br />    ....<br />    statement4;<br />    ....    <br />   END; <br />END<br /></pre>  | 

## Converting the WITH statement in Oracle to RDS for MySQL or Amazon Aurora MySQL<a name="CHAP_Source.Oracle.ToMySQL.With"></a>

You use the WITH clause \(subquery\_factoring\) in Oracle to assign a name \(query\_name\) to a subquery block\. You can then reference the subquery block multiple places in the query by specifying query\_name\. If a subquery block doesn't contain links or parameters \(local, procedure, function, package\), then AWS SCT converts the clause to a view or a temporary table\. 

The advantage of converting the clause to a temporary table is that repeated references to the subquery might be more efficient\. The greater efficiency is because the data is easily retrieved from the temporary table rather than being required by each reference\. You can emulate this by using additional views or a temporary table\. The view name uses the format `<procedure_name>$<subselect_alias>`\.

You can find examples in the table following\. 


| Oracle statement | MySQL statement | 
| --- | --- | 
|  <pre>CREATE PROCEDURE <br /> TEST_ORA_PG.P_WITH_SELECT_VARIABLE_01<br />     (p_state IN NUMBER)<br />AS<br />  l_dept_id NUMBER := 1; <br />BEGIN<br />FOR cur IN  <br />           (WITH dept_empl(id, name, surname, <br />              lastname, state, dept_id)<br />              AS<br />                  (<br />                    SELECT id, name, surname,  <br />                     lastname, state, dept_id <br />                      FROM test_ora_pg.dept_employees<br />                     WHERE state = p_state AND <br />                       dept_id = l_dept_id)<br />            SELECT id,state   <br />              FROM dept_empl<br />            ORDER BY id)  LOOP<br />  NULL;<br />END LOOP;<br /></pre>  |  <pre>CREATE PROCEDURE test_ora_pg.P_WITH_SELECT_VARIABLE_01(IN par_P_STATE DOUBLE)<br />BEGIN<br />    DECLARE var_l_dept_id DOUBLE DEFAULT 1;<br />    DECLARE var$id VARCHAR (8000);<br />    DECLARE var$state VARCHAR (8000);<br />    DECLARE done INT DEFAULT FALSE;<br />    DECLARE cur CURSOR FOR SELECT<br />        ID, STATE<br />        FROM (SELECT<br />            ID, NAME, SURNAME, LASTNAME, STATE, DEPT_ID<br />            FROM TEST_ORA_PG.DEPT_EMPLOYEES<br />            WHERE STATE = par_p_state AND DEPT_ID = var_l_dept_id) AS dept_empl<br />        ORDER BY ID;<br />    DECLARE CONTINUE HANDLER FOR NOT FOUND<br />        SET done := TRUE;<br />    OPEN cur;<br /><br />    read_label:<br />    LOOP<br />        FETCH cur INTO var$id, var$state;<br /><br />        IF done THEN<br />            LEAVE read_label;<br />        END IF;<br /><br />        BEGIN<br />        END;<br />    END LOOP;<br />    CLOSE cur;<br />END;<br /></pre>  | 
|  <pre>CREATE PROCEDURE <br /> TEST_ORA_PG.P_WITH_SELECT_REGULAR_MULT_01<br />AS    <br />BEGIN<br /><br /> FOR cur IN  (<br />               WITH dept_empl AS<br />                   (<br />                        SELECT id, name, surname, <br />                         lastname, state, dept_id <br />                          FROM test_ora_pg.dept_employees<br />                         WHERE state = 1),<br />                    dept AS <br />                   (SELECT id deptid, parent_id, <br />                      name deptname<br />                      FROM test_ora_pg.department                <br />                   )<br />                SELECT dept_empl.*,dept.*          <br />                 FROM dept_empl, dept<br />                 WHERE dept_empl.dept_id = dept.deptid<br />              ) LOOP<br />              NULL;<br />            END LOOP;<br /></pre>  |  <pre>CREATE VIEW TEST_ORA_PG.`P_WITH_SELECT_REGULAR_MULT_01$dept_empl<br /> `(id, name, surname, lastname, state, dept_id)<br />AS<br />(SELECT id, name, surname, lastname, state, dept_id <br />   FROM test_ora_pg.dept_employees<br />  WHERE state = 1);<br />  <br />CREATE VIEW TEST_ORA_PG.`P_WITH_SELECT_REGULAR_MULT_01$dept<br /> `(deptid, parent_id,deptname)<br />AS<br />(SELECT id deptid, parent_id, name deptname<br />   FROM test_ora_pg.department);  <br /><br /><br />CREATE PROCEDURE test_ora_pg.P_WITH_SELECT_REGULAR_MULT_01()<br />BEGIN<br />    DECLARE var$ID DOUBLE;<br />    DECLARE var$NAME VARCHAR (30);<br />    DECLARE var$SURNAME VARCHAR (30);<br />    DECLARE var$LASTNAME VARCHAR (30);<br />    DECLARE var$STATE DOUBLE;<br />    DECLARE var$DEPT_ID DOUBLE;<br />    DECLARE var$deptid DOUBLE;<br />    DECLARE var$PARENT_ID DOUBLE;<br />    DECLARE var$deptname VARCHAR (200);<br />    DECLARE done INT DEFAULT FALSE;<br />    DECLARE cur CURSOR FOR SELECT<br />        dept_empl.*, dept.*<br />        FROM TEST_ORA_PG.`P_WITH_SELECT_REGULAR_MULT_01$dept_empl<br />          ` AS dept_empl,<br />             TEST_ORA_PG.`P_WITH_SELECT_REGULAR_MULT_01$dept<br />          ` AS dept<br />        WHERE dept_empl.DEPT_ID = dept.DEPTID;<br />    DECLARE CONTINUE HANDLER FOR NOT FOUND<br />        SET done := TRUE;<br />    OPEN cur;<br /><br />    read_label:<br />    LOOP<br />    FETCH cur INTO var$ID, var$NAME, var$SURNAME, <br />     var$LASTNAME, var$STATE, var$DEPT_ID, var$deptid, <br />     var$PARENT_ID, var$deptname;<br /><br />        IF done THEN<br />            LEAVE read_label;<br />        END IF;<br /><br />        BEGIN<br />        END;<br />    END LOOP;<br />    CLOSE cur;<br />END;<br /><br />call test_ora_pg.P_WITH_SELECT_REGULAR_MULT_01()<br /></pre>  | 
|  <pre>CREATE PROCEDURE <br />  TEST_ORA_PG.P_WITH_SELECT_VAR_CROSS_02(p_state IN NUMBER)<br />AS    <br />   l_dept_id NUMBER := 10;<br />BEGIN<br /> FOR cur IN  (<br />               WITH emp AS              <br />                    (SELECT id, name, surname, <br />                      lastname, state, dept_id <br />                       FROM test_ora_pg.dept_employees<br />                      WHERE dept_id > 10                 <br />                    ),<br />                    active_emp AS<br />                    (<br />                      SELECT id<br />                        FROM emp<br />                       WHERE emp.state = p_state <br />                    )<br />                    <br />                SELECT *          <br />                  FROM active_emp                 <br />              ) LOOP<br />         NULL;<br />  END LOOP;<br />  <br />END;<br /></pre>  |  <pre>CREATE VIEW TEST_ORA_PG.`P_WITH_SELECT_VAR_CROSS_01$emp<br />    `(id, name, surname, lastname, state, dept_id)<br />AS<br />(SELECT<br />       id, name, surname, lastname, <br />       state, dept_id<br />  FROM TEST_ORA_PG.DEPT_EMPLOYEES<br />  WHERE DEPT_ID > 10);<br /><br /><br />CREATE PROCEDURE <br />   test_ora_pg.P_WITH_SELECT_VAR_CROSS_02(IN par_P_STATE DOUBLE)<br />BEGIN<br />    DECLARE var_l_dept_id DOUBLE DEFAULT 10;<br />    DECLARE var$ID DOUBLE;<br />    DECLARE done INT DEFAULT FALSE;<br />    DECLARE cur CURSOR FOR SELECT *<br />                             FROM (SELECT<br />                                      ID<br />                                     FROM <br />                             TEST_ORA_PG.<br />                              `P_WITH_SELECT_VAR_CROSS_01$emp` AS emp<br />                                   WHERE emp.STATE = par_p_state) <br />                                    AS active_emp;<br />    DECLARE CONTINUE HANDLER FOR NOT FOUND<br />        SET done := TRUE;<br />    OPEN cur;<br /><br />    read_label:<br />    LOOP<br />        FETCH cur INTO var$ID;<br /><br />        IF done THEN<br />            LEAVE read_label;<br />        END IF;<br /><br />        BEGIN<br />        END;<br />    END LOOP;<br />    CLOSE cur;<br />END;<br /></pre>  | 