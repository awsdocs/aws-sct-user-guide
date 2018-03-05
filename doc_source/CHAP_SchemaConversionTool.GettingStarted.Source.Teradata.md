# Connecting to a Teradata Source Database<a name="CHAP_SchemaConversionTool.GettingStarted.Source.Teradata"></a>

Use the following procedure to connect to your Teradata source database with the AWS Schema Conversion Tool \(AWS SCT\)\. 

**To connect to a Teradata source database**

1. In the AWS Schema Conversion Tool, choose **Connect to Teradata**\.   
![\[Connect to source database\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/file_connect_to_teradata.png)

   The **Connect to Teradata** dialog box appears\.  
![\[Teradata connection information\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/images/source-teradata.png)

1. Provide the Teradata source database connection information\. Use the instructions in the following table\.   
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_SchemaConversionTool.GettingStarted.Source.Teradata.html)

1. Choose **Test Connection** to verify that you can successfully connect to your source database\. 

1. Choose **OK** to connect to your source database\.

## Using LDAP Authentication with a Teradata Source<a name="CHAP_SchemaConversionTool.GettingStarted.Source.Teradata.LDAP"></a>

To set up Lightweight Directory Access Protocol \(LDAP\) authentication for Teradata users who run Microsoft Active Directory in Windows, use the following procedure\. 

In the procedure examples, the Active Directory domain is `test.local.com`\. The Windows server is `DC`, and it is configured with default settings\. The user account created in Active Directory is `test_ldap`, and the account uses the password `test_ldap`\.

1. In the `/opt/teradata/tdat/tdgss/site` directory, edit the file `TdgssUserConfigFile.xml` \. Change the LDAP section to the following\.

   ```
   AuthorizationSupported="no"
   
   LdapServerName="DC.test.local.com"
   LdapServerPort="389"
   LdapServerRealm="test.local.com"
   LdapSystemFQDN="dc= test, dc= local, dc=com"
   LdapBaseFQDN="dc=test, dc=local, dc=com"
   ```

   Apply the changes by running the configuration as follows\.

   ```
   #cd /opt/teradata/tdgss/bin
   #./run_tdgssconfig
   ```

1. Test the configuration by running the following command\.

   ```
   # /opt/teradata/tdat/tdgss/14.10.03.01/bin/tdsbind -u test_ldap -w test_ldap
   ```

   The output should be similar to the following\.

   ```
   LdapGroupBaseFQDN: dc=Test, dc=local, dc=com
   LdapUserBaseFQDN: dc=Test, dc=local, dc=com
   LdapSystemFQDN: dc= test, dc= local, dc=com
   LdapServerName: DC.test.local.com
   LdapServerPort: 389
   LdapServerRealm: test.local.com
   LdapClientUseTls: no
   LdapClientTlsReqCert: never
   LdapClientMechanism: SASL/DIGEST-MD5
   LdapServiceBindRequired: no
   LdapClientTlsCRLCheck: none
   LdapAllowUnsafeServerConnect: yes
   UseLdapConfig: no
   AuthorizationSupported: no
   FQDN: CN=test, CN=Users, DC=Anthem, DC=local, DC=com
   AuthUser: ldap://DC.test.local.com:389/CN=test1,CN=Users,DC=test,DC=local,DC=com
   DatabaseName: test
   Service: tdsbind
   ```

1. Restart TPA using the following command\.

   ```
   #tpareset -f "use updated TDGSSCONFIG GDO"                    
   ```

1. Create the same user in the Teradata database as in Active Directory, as shown following\.

   ```
   CREATE USER test_ldap AS PERM=1000, PASSWORD=test_ldap;
   GRANT LOGON ON ALL TO test WITH NULL PASSWORD;
   ```

If you change the user password in Active Directory for your LDAP user, you should specify this new password during connection to Teradata in LDAP mode\. In DEFAULT mode, you still have to connect Teradata with the LDAP user name and any password\.