set echo off
set termout on
set heading off
set feedback off
set trimspool on
set linesize 20026
set pagesize 200
set spool on
column vpath new_value new_vpath;
column dt new_value new_dt;
column tm new_value new_tm;
column ext new_value new_ext;
select to_char(sysdate,'-DD_MM_YYYY-') dt,to_char(SYSTIMESTAMP,'HH_MI_SS') tm,'.xml' ext from dual;
SELECT host_name vpath FROM v$instance;
Spool &new_vpath&new_dt&new_tm&new_ext;
Prompt	<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
Prompt	<Oracle12c xmlns:xsi="http://ww.w3.org/2001/XMLSchema-instance" version="1.7">
Prompt		<Control>
Prompt			<S_No>1</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:1</CIS_Number>
Prompt			<Control_Name>%ANY% is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database ANY keyword provides the user the capability to alter any item in the catalog of the database.</Control_Description>
Prompt			<Control_Risk>As authorization to use the ANY expansion of a privilege can allow an unauthorized user to potentially change confidential data or damage the data catalog, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure '%ANY%' Is Revoked from Unauthorized 'GRANTEE' REVOKE '[ANY Privilege]' FROM [grantee] </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE  FROM DBA_SYS_PRIVS  WHERE PRIVILEGE LIKE '%ANY%'  AND GRANTEE NOT IN ('AQ_ADMINISTRATOR_ROLE','DBA','DBSNMP','EXFSYS', 'EXP_FULL_DATABASE','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE', 'JAVADEBUGPRIV','MDSYS','OEM_MONITOR','OLAPSYS','OLAP_DBA','ORACLE_OCM', 'OWB$CLIENT','OWBSYS','SCHEDULER_ADMIN','SPATIAL_CSW_ADMIN_USR', 'SPATIAL_WFS_ADMIN_USR','SYS','SYSMAN','SYSTEM','WMSYS','APEX_030200', 'APEX_040000','APEX_040100','APEX_040200','LBACSYS', 'SYSBACKUP','CTXSYS','OUTLN','DVSYS','ORDPLUGINS','ORDSYS', 'GSMADMIN_INTERNAL','XDB','SYSDG','AUDIT_ADMIN','DV_OWNER','DV_REALM_OWNER', 'EM_EXPRESS_ALL', 'RECOVERY_CATALOG_OWNER');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement:
Prompt          SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE LIKE '%ANY%' AND GRANTEE NOT IN ('AQ_ADMINISTRATOR_ROLE','DBA','DBSNMP','EXFSYS','EXP_FULL_DATABASE','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE','JAVADEBUGPRIV','MDSYS','OEM_MONITOR','OLAPSYS','OLAP_DBA','ORACLE_OCM','OWB$CLIENT','OWBSYS','SCHEDULER_ADMIN','SPATIAL_CSW_ADMIN_USR','SPATIAL_WFS_ADMIN_USR','SYS','SYSMAN','SYSTEM','WMSYS','APEX_030200','APEX_040000','APEX_040100','APEX_040200','LBACSYS','SYSBACKUP','CTXSYS','OUTLN','DVSYS','ORDPLUGINS','ORDSYS',’RECOVERY_CATALOG_OWNER_VPD’,'GSMADMIN_INTERNAL','XDB','SYSDG','AUDIT_ADMIN','DV_OWNER','DV_REALM_OWNER','EM_EXPRESS_ALL','RECOVERY_CATALOG_OWNER','APEX_050000','SYSMAN_STB','SYSMAN_TYPES');
Prompt          2. To remediate this setting execute the following SQL statement:
Prompt          # REVOKE 'ANY Privilege' FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when '%ANY%' Is Revoked from Unauthorized GRANTEE</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE  FROM DBA_SYS_PRIVS  WHERE PRIVILEGE LIKE '%ANY%'  AND GRANTEE NOT IN ('AQ_ADMINISTRATOR_ROLE','DBA','DBSNMP','EXFSYS', 'EXP_FULL_DATABASE','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE', 'JAVADEBUGPRIV','MDSYS','OEM_MONITOR','OLAPSYS','OLAP_DBA','ORACLE_OCM', 'OWB$CLIENT','OWBSYS','SCHEDULER_ADMIN','SPATIAL_CSW_ADMIN_USR', 'SPATIAL_WFS_ADMIN_USR','SYS','SYSMAN','SYSTEM','WMSYS','APEX_030200', 'APEX_040000','APEX_040100','APEX_040200','LBACSYS', 'SYSBACKUP','CTXSYS','OUTLN','DVSYS','ORDPLUGINS','ORDSYS', 'GSMADMIN_INTERNAL','XDB','SYSDG','AUDIT_ADMIN','DV_OWNER','DV_REALM_OWNER', 'EM_EXPRESS_ALL', 'RECOVERY_CATALOG_OWNER'); 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>2</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:2</CIS_Number>
Prompt			<Control_Name>ALL is Revoked from Unauthorized 'GRANTEE' on 'AUD$'</Control_Name>
Prompt			<Control_Description>TThe Oracle database SYS.AUD$ table contains all the audit records for the database of the non Data Manipulation Language (DML) events, such as ALTER, DROP, CREATE, and so forth. (DML changes need trigger-based audit events to record data alterations.)</Control_Description>
Prompt			<Control_Risk>As permitting non-privileged users the authorization to manipulate the SYS_AUD$ table can allow distortion of the audit records, hiding unauthorized activities, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALL' Is Revoked from Unauthorized 'GRANTEE' on 'AUD$' REVOKE ALL ON AUD$ FROM [grantee]; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='AUD$' AND GRANTEE NOT IN ('DELETE_CATALOG_ROLE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. 
Prompt          SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='AUD$' AND GRANTEE NOT IN ('DELETE_CATALOG_ROLE');
Prompt       2. To remediate this setting execute the following SQL statement: 
Prompt      # REVOKE ALL ON AUD$ FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALL is not Revoked from Unauthorized 'GRANTEE' on 'AUD$'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='AUD$' AND GRANTEE NOT IN ('DELETE_CATALOG_ROLE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>3</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:3</CIS_Number>
Prompt			<Control_Name>ALL Is Revoked from Unauthorized 'GRANTEE' on 'DBA_%'</Control_Name>
Prompt			<Control_Description>The Oracle database DBA_ views show all information which is relevant to administrative accounts.</Control_Description>
Prompt			<Control_Risk>As permitting users the authorization to manipulate the DBA_ views can expose sensitive data.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALL' Is Revoked from Unauthorized 'GRANTEE' on 'DBA_%' REVOKE ALL ON DBA_ FROM [Non-DBA/SYS grantee]; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT * FROM DBA_TAB_PRIVS  WHERE TABLE_NAME LIKE 'DBA_%'  and GRANTEE NOT IN ('APEX_030200','APPQOSSYS','AQ_ADMINISTRATOR_ROLE','CTXSYS', 'EXFSYS','MDSYS','OLAP_XS_ADMIN','OLAPSYS','ORDSYS','OWB$CLIENT','OWBSYS', 'SELECT_CATALOG_ROLE','WM_ADMIN_ROLE','WMSYS','XDBADMIN','LBACSYS', 'ADM_PARALLEL_EXECUTE_TASK','CISSCANROLE','APEX_040200','SYSKM','ORACLE_OCM', 'DVSYS','GSMADMIN_INTERNAL','XDB','SYSDG','SYS','AUDIT_ADMIN', 'AUDIT_VIEWER', 'CAPTURE_ADMIN', 'DBA', 'DV_ACCTMGR', 'DV_MONITOR', 'DV_SECANALYST')</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt          'SELECT grantee||'.'||table_name FROM DBA_TAB_PRIVS WHERE TABLE_NAME LIKE 'DBA_%' AND GRANTEE NOT IN ('DBA','AUDIT_ADMIN','AUDIT_VIEWER','CAPTURE_ADMIN','DVSYS','SYSDG','DV_SECANALYST','SYSKM','DV_MONITOR','ORACLE_OCM','DV_ACCTMGR','GSMADMIN_INTERNAL','XDB','SYS','APPQOSSYS','AQ_ADMINISTRATOR_ROLE','CTXSYS','EXFSYS','MDSYS','OLAP_XS_ADMIN','OLAPSYS','ORDSYS','OWB$CLIENT','OWBSYS','SELECT_CATALOG_ROLE','WM_ADMIN_ROLE','WMSYS','XDBADMIN','LBACSYS',ADM_PARALLEL_EXECUTE_TASK','CISSCANROLE') AND NOT REGEXP_LIKE(grantee,'^APEX_0[3-9][0-9][0-9][0-9][0-9]$');
Prompt         2. Replace ltnon-DBA/SYS granteegt, in the query below, with the Oracle login(s) or role(s) returned from the associated audit procedure and execute: 
Prompt        #REVOKE ALL ON DBA_ FROM Non-DBA/SYS grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALL Is not Revoked from Unauthorized 'GRANTEE' on 'DBA_%'</Comments>
Prompt <Actual_Value>
SELECT * FROM DBA_TAB_PRIVS  WHERE TABLE_NAME LIKE 'DBA_%'  and GRANTEE NOT IN ('APEX_030200','APPQOSSYS','AQ_ADMINISTRATOR_ROLE','CTXSYS', 'EXFSYS','MDSYS','OLAP_XS_ADMIN','OLAPSYS','ORDSYS','OWB$CLIENT','OWBSYS', 'SELECT_CATALOG_ROLE','WM_ADMIN_ROLE','WMSYS','XDBADMIN','LBACSYS', 'ADM_PARALLEL_EXECUTE_TASK','CISSCANROLE','APEX_040200','SYSKM','ORACLE_OCM', 'DVSYS','GSMADMIN_INTERNAL','XDB','SYSDG','SYS','AUDIT_ADMIN', 'AUDIT_VIEWER', 'CAPTURE_ADMIN', 'DBA', 'DV_ACCTMGR', 'DV_MONITOR', 'DV_SECANALYST') AND NOT REGEXP_LIKE(grantee,'^APEX_0[3-9][0-9][0-9][0-9][0-9]$');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>4</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:4</CIS_Number>
Prompt			<Control_Name>ALL Is Revoked from Unauthorized 'GRANTEE' on 'LINK$'</Control_Name>
Prompt			<Control_Description>The Oracle database SYS.LINK$ table contains all the users password information and data table link information.</Control_Description>
Prompt			<Control_Risk>As permitting non-privileged users to manipulate or view the SYS.LINK$ table can allow capture of password information and/or corrupt the primary database linkages, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALL' Is Revoked from Unauthorized 'GRANTEE' on 'LINK$' REVOKE ALL ON LINK$ FROM [grantee]; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='LINK$' AND GRANTEE NOT IN ('DV_SECANALYST');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt          SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='LINK$' AND GRANTEE NOT IN ('DV_SECANALYST') AND OWNER='SYS';
Prompt          2. To remediate this setting execute the following SQL statement: 
Prompt         # REVOKE ALL ON LINK$ FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALL Is not Revoked from Unauthorized 'GRANTEE' on 'LINKS' </Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='LINK$' AND GRANTEE NOT IN ('DV_SECANALYST');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>5</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:5</CIS_Number>
Prompt			<Control_Name>ALL Is Revoked from Unauthorized 'GRANTEE' on 'SYS.SCHEDULER$_CREDENTIAL'</Control_Name>
Prompt			<Control_Description>The Oracle database SCHEDULER$_CREDENTIAL table contains the database scheduler credential information.</Control_Description>
Prompt			<Control_Risk>As permitting non-­privileged users the authorization to open the SYS.SCHEDULER$_CREDENTIAL table.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALL' Is Revoked from Unauthorized 'GRANTEE' on 'SYS.SCHEDULER$_CREDENTIAL'  REVOKE ALL ON SYS.SCHEDULER$_CREDENTIAL FROM [username];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='SCHEDULER$_CREDENTIAL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt      SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='SCHEDULER$_CREDENTIAL' AND OWNER='SYS';
Prompt  2. To remediate this setting execute the following SQL statement: 
Prompt  # REVOKE ALL ON SYS.SCHEDULER$_CREDENTIAL FROM [username];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALL Is not Revoked from Unauthorized 'GRANTEE' on 'SYS.SCHEDULER$_CREDENTIAL' </Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='SCHEDULER$_CREDENTIAL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>6</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:6</CIS_Number>
Prompt			<Control_Name>ALL Is Revoked from Unauthorized 'GRANTEE' on 'SYS.USER$'</Control_Name>
Prompt			<Control_Description>The Oracle database SYS.USER$ table contains the users hashed password information.</Control_Description>
Prompt			<Control_Risk>As permitting non-privileged users the authorization to open the SYS.USER$ table can allow the capture of password hashes for the later application of password cracking algorithms to breach confidentiality, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALL' Is Revoked from Unauthorized 'GRANTEE' on 'SYS.USER$' REVOKE ALL ON SYS.USER$ FROM [username]	;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER$' AND GRANTEE NOT IN ('DV_SECANALYST', 'DVSYS', 'CTXSYS','XDB','APEX_030200', 'APEX_040000','APEX_040100','APEX_040200','ORACLE_OCM');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt  SELECT GRANTEE, PRIVILEGE
Prompt  FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER$' AND OWNER='SYS' AND GRANTEE NOT IN ('CTXSYS','XDB','APEX_030200','SYSMAN','APEX_040000','APEX_040100','APEX_040200','DV_SECANALYST','DVSYS','ORACLE_OCM');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE ALL ON SYS.USER$ FROM username;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALL Is not Revoked from Unauthorized 'GRANTEE' on 'SYS.USER$'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER$' AND GRANTEE NOT IN ('DV_SECANALYST', 'DVSYS', 'CTXSYS','XDB','APEX_030200', 'APEX_040000','APEX_040100','APEX_040200','ORACLE_OCM');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>7</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:7</CIS_Number>
Prompt			<Control_Name>ALL Is Revoked from Unauthorized 'GRANTEE' on 'USER_HISTORY$'</Control_Name>
Prompt			<Control_Description>The Oracle database SYS.USER_HISTORY$ table contains all the audit records for the users password change history. (This table gets updated by password changes if the user has an assigned profile that has password reuse limit set, e.g., PASSWORD_REUSE_TIME set to other than UNLIMITED.)</Control_Description>
Prompt			<Control_Risk>As permitting non-privileged users the authorization to manipulate the records in the SYS.USER_HISTORY$ table can allow distortion of the audit trail, potentially hiding unauthorized data confidentiality attacks or integrity changes, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALL is Revoked from Unauthorized 'GRANTEE' REVOKE ALL ON USER_HISTORY$ FROM grantee;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER_HISTORY$';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt  SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER_HISTORY$' AND OWNER = 'SYS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE ALL ON USER_HISTORY$ FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt       <Comments>Control becomes NON-COMPLIANT when ALL Is not Revoked from Unauthorized 'GRANTEE' on 'USER_HISTORY$'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_TAB_PRIVS WHERE TABLE_NAME='USER_HISTORY$';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>8</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:8</CIS_Number>
Prompt			<Control_Name>All Sample Data And Users Have Been Removed</Control_Name>
Prompt			<Control_Description>Oracle sample schemas are not needed for the operation of the database. These include, among others, information pertaining to a sample schemas pertaining to Human Resources, Business Intelligence, Order Entry, and the like. These samples create sample users (BI,HR,OE,PM,IX,SH, SCOTT), in addition to tables and fictitious data</Control_Description>
Prompt			<Control_Risk>The sample data is typically not required for production operations of the database and provides users with well-known default passwords, particular views, and procedures/functions. Such users, views, and/or procedures/functions could be used to launch exploits against production environments</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure All Sample Data And Users Have Been Removed # $ORACLE_HOME/demo/schema/drop_sch.sql# DROP USER SCOTT CASCADE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT USERNAME FROM ALL_USERS WHERE USERNAME IN ('BI','HR','IX','OE','PM','SCOTT','SH');  NOTE: The Oracle sample user names may be in use on a production basis. It is important that you first verify that BI, HR, IX, OE, PM, SCOTT, and/or SH are not valid production user names before executing the dropping SQL scripts.</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, check for the presence of Oracle sample users by executing the following SQL statement.
Prompt SELECT USERNAME FROM ALL_USERS WHERE USERNAME IN ('BI','HR','IX','OE','PM','SCOTT','SH');
Prompt 2. To remediate this setting, it is recommended that you execute the following SQL script:
Prompt # $ORACLE_HOME/demo/schema/drop_sch.sql
Prompt 3. Then, execute the following SQL statement.
Prompt # DROP USER SCOTT CASCADE; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt        <Comments>Control becomes NON-COMPLIANT when ALL Sample Data and Users have not been removed.</Comments>
Prompt <Actual_Value>
SELECT USERNAME FROM ALL_USERS WHERE USERNAME IN ('BI','HR','IX','OE','PM','SCOTT','SH');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>9</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:9</CIS_Number>
Prompt			<Control_Name>ALTER SYSTEM Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database ALTER SYSTEM privilege allows the designated user to dynamically alter the instance running operations.</Control_Description>
Prompt			<Control_Risk>As assignment of the ALTER SYSTEM privilege can lead to severe problems, such as the instances session being killed or the stopping of redo log recording, which would make transactions unrecoverable, this capability should be severely restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALTER SYSTEM' Is Revoked from Unauthorized 'GRANTEE' REVOKE ALTER SYSTEM FROM  [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='ALTER SYSTEM' AND GRANTEE NOT IN ('SYSBACKUP', 'EM_EXPRESS_ALL', 'GSMADMIN_ROLE', 'GSMADMIN_INTERNAL', 'SYSDG', 'SYS','SYSTEM','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','DBA','EM_EXPRESS_ALL','SYSBACKUP','GSMADMIN_ROLE','GSM_INTERNAL','SYSDG','GSMADMIN_INTERNAL');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement: 
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='ALTER SYSTEM' AND GRANTEE NOT IN ('SYS','SYSTEM','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','DBA','EM_EXPRESS_ALL','SYSBACKUP','GSMADMIN_ROLE', 'GSM_INTERNAL','SYSDG','GSMADMIN_INTERNAL');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE ALTER SYSTEM FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt       <Comments>Control becomes NON-COMPLIANT when ALTER SYSTEM Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='ALTER SYSTEM' AND GRANTEE NOT IN ('SYSBACKUP', 'EM_EXPRESS_ALL', 'GSMADMIN_ROLE', 'GSMADMIN_INTERNAL', 'SYSDG', 'SYS','SYSTEM','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','DBA','EM_EXPRESS_ALL','SYSBACKUP','GSMADMIN_ROLE','GSM_INTERNAL','SYSDG','GSMADMIN_INTERNAL');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>10</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:10</CIS_Number>
Prompt			<Control_Name>AUDIT SYSTEM Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database AUDIT SYSTEM privilege allows the change auditing activities on the system.</Control_Description>
Prompt			<Control_Risk>As assignment of the AUDIT SYSTEM privilege can allow the unauthorized alteration of system audit activities, disabling the creation of audit trails, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'AUDIT SYSTEM' Is Revoked from Unauthorized 'GRANTEE' REVOKE AUDIT SYSTEM FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='AUDIT SYSTEM' AND GRANTEE NOT IN ('AUDIT_ADMIN','DBA','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE','SYS');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To asses this recommendation, execute the following SQL statement.
Prompt # SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='AUDIT SYSTEM' AND GRANTEE NOT IN ('DBA','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE', 'SYS','AUDIT_ADMIN');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt  # REVOKE AUDIT SYSTEM FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt       <Comments>Control becomes NON-COMPLIANT when AUDIT SYSTEM Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='AUDIT SYSTEM' AND GRANTEE NOT IN ('AUDIT_ADMIN','DBA','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE','SYS');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>11</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:11</CIS_Number>
Prompt			<Control_Name>BECOME USER Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database BECOME USER privilege allows the designated user to inherit the rights of another user.</Control_Description>
Prompt			<Control_Risk>As assignment of the BECOME USER privilege can allow the unauthorized use of another users privileges, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'BECOME USER' Is Revoked from Unauthorized 'GRANTEE' REVOKE BECOME USER FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');
Prompt 2. To remediate this setting execute the following SQL statement:
Prompt # REVOKE BECOME USER FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt <Comments>Control becomes NON-COMPLIANT when BECOME USER Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>12</S_No>
Prompt			<Category>Authentication and Authorization</Category>	
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:12</CIS_Number>
Prompt			<Control_Name>BECOME USER Is Revoked from Unauthorized 'ITGRANTEEGT'</Control_Name>
Prompt			<Control_Description>The Oracle database BECOME USER privilege allows the designated user to inherit the rights of another user.</Control_Description>
Prompt			<Control_Risk>As assignment of the BECOME USER privilege can allow the unauthorized use of another users privileges, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'BECOME USER' Is Revoked from Unauthorized 'GRANTEE' REVOKE BECOME USER FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE BECOME USER FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt <Comments>Control becomes NON-COMPLIANT when BECOME USER Is not Revoked from Unauthorized 'ITGRANTEEGT'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='BECOME USER' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>13</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:13</CIS_Number>
Prompt			<Control_Name>CREATE ANY LIBRARY Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database CREATE ANY LIBRARY privilege allows the designated user to create objects that are associated to the shared libraries.</Control_Description>
Prompt			<Control_Risk>As assignment of the CREATE ANY LIBRARY privilege can allow the creation of numerous library-associated objects and potentially corrupt the libraries integrity, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'CREATE ANY LIBRARY' Is Revoked from Unauthorized 'GRANTEE' REVOKE CREATE ANY LIBRARY FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE ANY LIBRARY' AND GRANTEE NOT IN ('SYS','SYSTEM','DBA', 'IMP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt          SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE ANY LIBRARY' AND GRANTEE NOT IN ('SYS','SYSTEM','DBA','IMP_FULL_DATABASE');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE CREATE ANY LIBRARY FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when  CREATE ANY LIBRARY Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE ANY LIBRARY' AND GRANTEE NOT IN ('SYS','SYSTEM','DBA', 'IMP_FULL_DATABASE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>14</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:14</CIS_Number>
Prompt			<Control_Name>CREATE LIBRARY Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database CREATE LIBRARY privilege allows the designated user to create objects that are associated to the shared libraries.</Control_Description>
Prompt			<Control_Risk>As assignment of the CREATE LIBRARY privilege can allow the creation of numerous library- associated objects and potentially corrupt the libraries integrity, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'CREATE LIBRARY' Is Revoked from Unauthorized 'GRANTEE' REVOKE CREATE ANY LIBRARY FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE LIBRARY' AND GRANTEE NOT IN ('GSMADMIN_INTERNAL', 'DVSYS', 'SYS','SYSTEM','DBA','SPATIAL_CSW_ADMIN_USR', 'XDB', 'EXFSYS', 'MDSYS', 'SPATIAL_WFS_ADMIN_USR');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE LIBRARY' AND GRANTEE NOT IN ('SYS','SYSTEM','DBA','MDSYS','SPATIAL_WFS_ADMIN_USR', 'SPATIAL_CSW_ADMIN_USR','DVSYS','GSMADMIN_INTERNAL','XDB');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE CREATE LIBRARY FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when CREATE LIBRARY Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE LIBRARY' AND GRANTEE NOT IN ('GSMADMIN_INTERNAL', 'DVSYS', 'SYS','SYSTEM','DBA','SPATIAL_CSW_ADMIN_USR', 'XDB', 'EXFSYS', 'MDSYS', 'SPATIAL_WFS_ADMIN_USR');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>15</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:15</CIS_Number>
Prompt			<Control_Name>CREATE_PROCEDURE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database CREATE PROCEDURE privilege allows the designated user to create a stored procedure that will fire when given the correct command sequence.</Control_Description>
Prompt			<Control_Risk>As assignment of the CREATE PROCEDURE privilege can lead to severe problems in unauthorized hands, such as rogue procedures facilitating data theft or Denial-of-Service by corrupting data tables, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'CREATE_PROCEDURE' Is Revoked from Unauthorized 'GRANTEE' REVOKE CREATE PROCEDURE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE PROCEDURE' AND GRANTEE NOT IN ('DVF','DV_REALM_RESOURCE','APEX_GRANTS_FOR_NEW_USERS_ROLE', 'DBA','DBSNMP','MDSYS','OLAPSYS','OWB$CLIENT', 'OWBSYS','RECOVERY_CATALOG_OWNER','SPATIAL_CSW_ADMIN_USR', 'SPATIAL_WFS_ADMIN_USR','SYS','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','RESOURCE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE PROCEDURE' AND GRANTEE NOT IN ( 'DBA','DBSNMP','MDSYS','OLAPSYS','OWB$CLIENT', 'OWBSYS','RECOVERY_CATALOG_OWNER','SPATIAL_CSW_ADMIN_USR','SPATIAL_WFS_ADMIN_USR','SYS','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','DVF','RESOURCE','DV_REALM_RESOURCE', 'APEX_GRANTS_FOR_NEW_USERS_ROLE','APEX_050000','MGMT_VIEW','SYSMAN_MDS','SYSMAN_OPSS','SYSMAN_RO','SYSMAN_STB');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE CREATE PROCEDURE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when CREATE_PROCEDURE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='CREATE PROCEDURE' AND GRANTEE NOT IN ('DVF','DV_REALM_RESOURCE','APEX_GRANTS_FOR_NEW_USERS_ROLE', 'DBA','DBSNMP','MDSYS','OLAPSYS','OWB$CLIENT', 'OWBSYS','RECOVERY_CATALOG_OWNER','SPATIAL_CSW_ADMIN_USR', 'SPATIAL_WFS_ADMIN_USR','SYS','APEX_030200','APEX_040000', 'APEX_040100','APEX_040200','RESOURCE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>16</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:16</CIS_Number>
Prompt			<Control_Name>DBA Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database DBA role is the default database administrator role provided for the allocation of administrative privileges.</Control_Description>
Prompt			<Control_Risk>As assignment of the DBA role to an ordinary user can provide a great number of unnecessary privileges to that user and opens the door to data breaches, integrity violations, and Denial-of-Service conditions, application of this role should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DBA' Is Revoked from Unauthorized 'GRANTEE' REVOKE DBA FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTED_ROLE='DBA' AND GRANTEE NOT IN ('SYS','SYSTEM');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTED_ROLE='DBA' AND GRANTEE NOT IN ('SYS','SYSTEM');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE DBA FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DBA Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTED_ROLE='DBA' AND GRANTEE NOT IN ('SYS','SYSTEM');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>17</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:17</CIS_Number>
Prompt			<Control_Name>DBA_SYS_PRIVS.% Is Revoked from Unauthorized 'GRANTEE' with 'ADMIN_OPTION' Set to 'YES'</Control_Name>
Prompt			<Control_Description>The Oracle database WITH_ADMIN privilege allows the designated user to grant another user the same privileges.</Control_Description>
Prompt			<Control_Risk>As assignment of the WITH_ADMIN privilege can allow the granting of a restricted privilege to an unauthorized user, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DBA_SYS_PRIVS.%' Is Revoked from Unauthorized 'GRANTEE' with 'ADMIN_OPTION' Set to 'YES' REVOKE [privilege] FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE ADMIN_OPTION='YES' AND GRANTEE not in ('DV_ACCTMGR', 'DVSYS', 'SYSKM', 'AQ_ADMINISTRATOR_ROLE','DBA','OWBSYS', 'SCHEDULER_ADMIN','SYS','SYSTEM','WMSYS') AND NOT REGEXP_LIKE(grantee,'^APEX_0[3-9][0-9][0-9][0-9][0-9]$');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE ADMIN_OPTION='YES' AND GRANTEE not in ('AQ_ADMINISTRATOR_ROLE','DBA','OWBSYS', 'SCHEDULER_ADMIN','SYS','SYSTEM','WMSYS','DVSYS','SYSKM','DV_ACCTMGR') AND NOT REGEXP_LIKE(grantee,'^APEX_0[3-9][0-9][0-9][0-9][0-9]$');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE [privilege] FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DBA_SYS_PRIVS.% Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE ADMIN_OPTION='YES' AND GRANTEE not in ('DV_ACCTMGR', 'DVSYS', 'SYSKM', 'AQ_ADMINISTRATOR_ROLE','DBA','OWBSYS', 'SCHEDULER_ADMIN','SYS','SYSTEM','WMSYS') AND NOT REGEXP_LIKE(grantee,'^APEX_0[3-9][0-9][0-9][0-9][0-9]$');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>18</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:18</CIS_Number>
Prompt			<Control_Name>DELETE_CATALOG_ROLE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database DELETE_CATALOG_ROLE provides DELETE privileges for the records in the systems audit table (AUD$).</Control_Description>
Prompt			<Control_Risk>As permitting unauthorized access to the DELETE_CATALOG_ROLE can allow the destruction of audit records vital to the forensic investigation of unauthorized activities, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DELETE_CATALOG_ROLE' Is Revoked from Unauthorized 'GRANTEE' REVOKE DELETE_CATALOG_ROLE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='DELETE_CATALOG_ROLE' AND GRANTEE NOT IN ('DBA','SYS');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='DELETE_CATALOG_ROLE' AND GRANTEE NOT IN ('DBA','SYS');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE DELETE_CATALOG_ROLE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DELETE_CATALOG_ROLE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='DELETE_CATALOG_ROLE' AND GRANTEE NOT IN ('DBA','SYS');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>19</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:19</CIS_Number>
Prompt			<Control_Name>Ensure No Users Are Assigned the 'DEFAULT' Profile</Control_Name>
Prompt			<Control_Description>Upon creation database users are assigned to the DEFAULT profile unless otherwise specified.</Control_Description>
Prompt			<Control_Risk>It is recommended that users be created with function-appropriate profiles. The DEFAULT profile, being defined by Oracle, is subject to change at any time (e.g. by patch or version update). The DEFAULT profile has unlimited settings that are often required by the SYS user when patching; such unlimited settings should be tightly reserved and not applied to unnecessary users.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure No Users Are Assigned the 'DEFAULT' Profile ALTER USER [username] PROFILE [appropriate_profile]</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT USERNAME FROM DBA_USERS WHERE PROFILE='DEFAULT' AND ACCOUNT_STATUS='OPEN' AND USERNAME NOT IN ('ANONYMOUS', 'CTXSYS', 'DBSNMP', 'EXFSYS', 'LBACSYS', 'MDSYS', 'MGMT_VIEW','OLAPSYS','OWBSYS', 'ORDPLUGINS', 'ORDSYS', 'OUTLN', 'SI_INFORMTN_SCHEMA','SYS', 'SYSMAN', 'SYSTEM', 'TSMSYS', 'WK_TEST', 'WKSYS', 'WKPROXY', 'WMSYS', 'XDB', 'CISSCAN');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt # SELECT USERNAME FROM DBA_USERS WHERE PROFILE='DEFAULT' AND ACCOUNT_STATUS='OPEN' AND USERNAME NOT IN ('ANONYMOUS', 'CTXSYS', 'DBSNMP', 'EXFSYS', 'LBACSYS','MDSYS', 'MGMT_VIEW','OLAPSYS','OWBSYS', 'ORDPLUGINS', 'ORDSYS', 'OUTLN', 'SI_INFORMTN_SCHEMA','SYS', 'SYSMAN', 'SYSTEM', 'TSMSYS', 'WK_TEST', 'WKSYS', 'WKPROXY', 'WMSYS', 'XDB', 'CISSCAN');
Prompt 2. To remediate this recommendation execute the following SQL statement for each user returned by the audit query using a functional-appropriate profile:
Prompt # ALTER USER username PROFILE appropriate_profile</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Users are Assigned the 'DEFAULT' Profile.</Comments>
Prompt <Actual_Value>
SELECT USERNAME FROM DBA_USERS WHERE PROFILE='DEFAULT' AND ACCOUNT_STATUS='OPEN' AND USERNAME NOT IN ('ANONYMOUS', 'CTXSYS', 'DBSNMP', 'EXFSYS', 'LBACSYS', 'MDSYS', 'MGMT_VIEW','OLAPSYS','OWBSYS', 'ORDPLUGINS', 'ORDSYS', 'OUTLN', 'SI_INFORMTN_SCHEMA','SYS', 'SYSMAN', 'SYSTEM', 'TSMSYS', 'WK_TEST', 'WKSYS', 'WKPROXY', 'WMSYS', 'XDB', 'CISSCAN');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>20</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:20</CIS_Number>
Prompt			<Control_Name>'EXECUTE ANY PROCEDURE' Is Revoked from 'DBSNMP'</Control_Name>
Prompt			<Control_Description>Remove unneeded privileges from DBSNMP</Control_Description>
Prompt			<Control_Risk>Migrated DBSNMP users have more privileges than required.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE ANY PROCEDURE' Is Revoked from 'DBSNMP' REVOKE EXECUTE ANY PROCEDURE FROM DBSNMP;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='DBSNMP';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='DBSNMP';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ANY PROCEDURE FROM DBSNMP;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE ANY PROCEDURE Is not Revoked from 'DBSNMP'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='DBSNMP';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>21</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:21</CIS_Number>
Prompt			<Control_Name>EXECUTE ANY PROCEDURE Is Revoked from 'OUTLN'</Control_Name>
Prompt			<Control_Description>Remove unneeded privileges from OUTLN</Control_Description>
Prompt			<Control_Risk>Migrated OUTLN users have more privileges than required.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE ANY PROCEDURE' Is Revoked from 'OUTLN' REVOKE EXECUTE ANY PROCEDURE FROM OUTLN;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='OUTLN';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='OUTLN';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ANY PROCEDURE FROM OUTLN;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE ANY PROCEDURE Is not Revoked from 'OUTLN'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXECUTE ANY PROCEDURE' AND GRANTEE='OUTLN';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>22</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:22</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_ADVISOR'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_ADVISOR package can be used to write files located on the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_ADVISOR package could allow an unauthorized user to corrupt operating system files on the instances host, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_ADVISOR' REVOKE EXECUTE ON DBMS_ADVISOR FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_ADVISOR';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_ADVISOR';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_ADVISOR FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_ADVISOR'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_ADVISOR';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>23</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:23</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_AQADM_SYS'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_AQADM_SYS package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_AQADM_SYS package could allow an unauthorized user to run SQL commands as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_AQADM_SYS' REVOKE EXECUTE ON DBMS_AQADM_SYS FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_AQADM_SYS FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_AQADM_SYS'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>24</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:24</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_AQADM_SYSCALLS'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_AQADM_SYSCALLS package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_AQADM_SYSCALLS package could allow an unauthorized user to run SQL commands as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_AQADM_SYSCALLS' REVOKE EXECUTE ON DBMS_AQADM_SYSCALLS FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYSCALLS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYSCALLS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_AQADM_SYSCALLS FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_AQADM_SYSCALLS'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_AQADM_SYSCALLS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>25</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:25</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_BACKUP_RESTORE'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_RANDOM package is used for generating random numbers but should not be used for cryptographic purposes.</Control_Description>
Prompt			<Control_Risk>As assignment of use of the DBMS_RANDOM package can allow the unauthorized application of the random number-generating function, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_BACKUP_RESTORE' REVOKE EXECUTE ON DBMS_BACKUP_RESTORE FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_BACKUP_RESTORE';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_BACKUP_RESTORE';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_BACKUP_RESTORE FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_BACKUP_RESTORE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_BACKUP_RESTORE';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>26</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:26</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_CRYPTO'</Control_Name>
Prompt			<Control_Description>The DBMS_CRYPTO settings provide a toolset that determines the strength of the encryption algorithm used to encrypt application data and is part of the SYS schema. The DES (56-bit key), 3DES (168-bit key), 3DES-2KEY (112-bit key), AES (128/192/256-bit keys), and RC4 are available.</Control_Description>
Prompt			<Control_Risk>As execution of these cryptography procedures by the user PUBLIC can potentially endanger portions of or all of the data storage, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_CRYPTO' REVOKE EXECUTE ON DBMS_CRYPTO FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND TABLE_NAME='DBMS_CRYPTO';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND TABLE_NAME='DBMS_CRYPTO';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_CRYPTO FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_CRYPTO'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND TABLE_NAME='DBMS_CRYPTO';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>27</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:27</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_FILE_TRANSFER'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_FILE_TRANSFER package allows to transfer files from one database server to another.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_FILE_TRANSFER package could allow to transfer files from one database server to another.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_FILE_TRANSFER' REVOKE EXECUTE ON DBMS_FILE_TRANSFER FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_FILE_TRANSFER';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_FILE_TRANSFER'; 
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt REVOKE EXECUTE ON DBMS_FILE_TRANSFER FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_FILE_TRANSFER'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_FILE_TRANSFER';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>28</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:28</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_IJOB'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_IJOB package is shipped as undocumented and allows to run database jobs in the context of another user.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_IJOB package could allow an attacker to change identities by using a different username to execute a database job.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_IJOB' REVOKE EXECUTE ON DBMS_IJOB FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_IJOB';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_IJOB';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_IJOB FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_IJOB'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_IJOB';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>29</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:29</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_JAVA'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_JAVA package can run Java classes (e.g. OS commands) or grant Java privileges.</Control_Description>
Prompt			<Control_Risk>The DBMS_JAVA package could allow an attacker to run operating system commands from the database.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_JAVA' REVOKE EXECUTE ON DBMS_JAVA FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_JAVA FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_JAVA'</Comments>

Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>30</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:30</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_JAVA_TEST'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_JAVA_TEST package can run Java classes (e.g. OS commands) or grant Java privileges.</Control_Description>
Prompt			<Control_Risk>The DBMS_JAVA_TEST package could allow an attacker to run operating system commands from the database..</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_JAVA_TEST' REVOKE EXECUTE ON DBMS_JAVA_TEST FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA_TEST'</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA_TEST';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_JAVA_TEST FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_JAVA_TEST'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JAVA_TEST';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>31</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:31</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_JOB'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_JOB package schedules and manages the jobs sent to the job queue and has been superseded by the DBMS_SCHEDULER package, even though DBMS_JOB has been retained for backwards compatibility.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_JOB package could allow an unauthorized user to disable or overload the job queue and has been superseded by the DBMS_SCHEDULER package, this package should be disabled or restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_JOB' REVOKE EXECUTE ON DBMS_JOB FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JOB';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JOB';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_JOB FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_JOB'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_JOB';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>32</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:32</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_LDAP'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_LDAP package contains functions and procedures that enable programmers to access data from LDAP servers.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_LDAP package can be used to create specially crafted error messages or send information via DNS to the outside.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_LDAP' REVOKE EXECUTE ON DBMS_LDAP FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LDAP';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LDAP';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt REVOKE EXECUTE ON DBMS_LDAP FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_LDAP'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LDAP';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>33</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:33</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_LOB'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_LOB package provides subprograms that can manipulate and read/write on BLOBs, CLOBs, NCLOBs, BFILEs, and+ temporary LOBs.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_LOB package could allow an unauthorized user to manipulate BLOBs, CLOBs, NCLOBs, BFILEs, and temporary LOBs on the instance, either destroying data or causing a Denial-of-Service condition due to corruption of disk space, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_LOB' REVOKE EXECUTE ON DBMS_LOB FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LOB';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LOB';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_LOB FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_LOB'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_LOB';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>34</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:34</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_OBFUSCATION_TOOLKIT'</Control_Name>
Prompt			<Control_Description>The DBMS_OBFUSCATION_TOOLKIT settings provide one of the tools that determine the strength of the encryption algorithm used to encrypt application data and is part of the SYS schema. The DES (56-bit key) and 3DES (168-bit key) are the only two types available.</Control_Description>
Prompt			<Control_Risk>As allowing the PUBLIC user privileges to access this capability can be potentially harm the data storage, this access should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_OBFUSCATION_TOOLKIT' REVOKE EXECUTE ON DBMS_OBFUSCATION_TOOLKIT FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_OBFUSCATION_TOOLKIT';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_OBFUSCATION_TOOLKIT';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_OBFUSCATION_TOOLKIT FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_OBFUSCATION_TOOLKIT'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_OBFUSCATION_TOOLKIT';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>35</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:35</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_PRVTAQIM'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_PRVTAQIM package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_PRVTAQIM package could allow an unauthorized user to escalate privileges because any SQL statements could be executed as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_PRVTAQIM' REVOKE EXECUTE ON DBMS_PRVTAQIM FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_PRVTAQIM';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_PRVTAQIM';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt REVOKE EXECUTE ON DBMS_PRVTAQIM FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_PRVTAQIM'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_PRVTAQIM';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>36</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:36</CIS_Number>
Prompt			<Control_Name>EXECUTE is Revoked from 'PUBLIC' on 'DBMS_RANDOM'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_RANDOM package is used for generating random numbers but should not be used for cryptographic purposes.</Control_Description>
Prompt			<Control_Risk>As assignment of use of the DBMS_RANDOM package can allow the unauthorized application of the random number generating function, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_RANDOM' REVOKE EXECUTE ON DBMS_RANDOM FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_RANDOM';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_RANDOM';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_RANDOM FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_RANDOM'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_RANDOM';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>37</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:37</CIS_Number>
Prompt			<Control_Name>EXECUTE is Revoked from 'PUBLIC' on 'DBMS_REPCAT_SQL_UTL'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_REPACT_SQL_UTL package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_REPACT_SQL_UTL package could allow an unauthorized user to run SQL commands as user SYS</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_REPCAT_SQL_UTL' revoke execute on DBMS_REPCAT_SQL_UTL FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_REPCAT_SQL_UTL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_REPCAT_SQL_UTL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # revoke execute on DBMS_REPCAT_SQL_UTL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_REPCAT_SQL_UTL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_REPCAT_SQL_UTL'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>38</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:38</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_SCHEDULER'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_SCHEDULER package schedules and manages the database and operating system jobs .</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_SCHEDULER package could allow an unauthorized user to run database or operating system jobs.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_SCHEDULER' REVOKE EXECUTE ON DBMS_SCHEDULER FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SCHEDULER';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SCHEDULER';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_SCHEDULER FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_SCHEDULER'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SCHEDULER';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>39</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:39</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_SQL'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_SQL package is used for running dynamic SQL statements.</Control_Description>
Prompt			<Control_Risk>The DBMS_SQL package could allow privilege escalation if the input validation is not done properly.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_SQL' REVOKE EXECUTE ON DBMS_SQL FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SQL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SQL';

Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_SQL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_SQL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SQL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>40</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:40</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_STREAMS_ADM_UTL'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_STREAMS_ADM_UTL package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_STREAMS_ADM_UTL package could allow an unauthorized user to run SQL commands as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value> Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_STREAMS_ADM_UTL' REVOKE EXECUTE ON DBMS_STREAMS_ADM_UTL FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_ADM_UTL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_ADM_UTL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_STREAMS_ADM_UTL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_STREAMS_ADM_UTL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_ADM_UTL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>41</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:41</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_STREAMS_RPC'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_STREAMS_RPC package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_STREAMS_RPC package could allow an unauthorized user to run SQL commands as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_STREAMS_RPC' REVOKE EXECUTE ON DBMS_STREAMS_RPC FROM PUBLIC;;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_RPC';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_RPC';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_STREAMS_RPC FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_STREAMS_RPC'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_STREAMS_RPC';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>42</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:42</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_SYS_SQL'</Control_Name>
Prompt			<Control_Description>The Oracle database DBMS_SYS_SQL package is shipped as undocumented.</Control_Description>
Prompt			<Control_Risk>As use of the DBMS_SYS_SQL package could allow an user to run code as a different user without entering user credentials.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_SYS_SQL' REVOKE EXECUTE ON DBMS_SYS_SQL FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SYS_SQL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SYS_SQL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_SYS_SQL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_SYS_SQL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_SYS_SQL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>43</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:43</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_XMLGEN'</Control_Name>
Prompt			<Control_Description>The DBMS_XMLGEN package takes an arbitrary SQL query as input, converts it to XML format, and returns the result as a CLOB.</Control_Description>
Prompt			<Control_Risk>The package DBMS_XMLGEN can be used to search the entire database for critical information like credit card numbers, and other sensitive information.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_XMLGEN' REVOKE EXECUTE ON DBMS_XMLGEN FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLGEN';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLGEN';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_XMLGEN FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_XMLGEN'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLGEN';
Prompt </Actual_Value>

Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>44</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:44</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'DBMS_XMLQUERY'</Control_Name>
Prompt			<Control_Description>The Oracle package DBMS_XMLQUERY takes an arbitrary SQL query, converts it to XML format, and returns the result. This package is similar to DBMS_XMLGEN.</Control_Description>
Prompt			<Control_Risk>The package DBMS_XMLQUERY can be used to search the entire database for critical information like credit card numbers and other sensitive information.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'DBMS_XMLQUERY' REVOKE EXECUTE ON DBMS_XMLQUERY FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLQUERY';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLQUERY';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON DBMS_XMLQUERY FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'DBMS_XMLQUERY'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='DBMS_XMLQUERY';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>45</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:45</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'HTTPURITYPE'</Control_Name>
Prompt			<Control_Description>The Oracle database HTTPURITYPE object type can be used to perform HTTP-requests.</Control_Description>
Prompt			<Control_Risk>The ability to perform HTTP requests could be used to leak information from the database to an external destination.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'HTTPURITYPE' REVOKE EXECUTE ON HTTPURITYPE FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='HTTPURITYPE';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='HTTPURITYPE';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON HTTPURITYPE FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'HTTPURITYPE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='HTTPURITYPE';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>46</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>4.2.5</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'INITJVMAUX'</Control_Name>
Prompt			<Control_Description>The Oracle database INITJVMAUX package is shipped as undocumented and allows to run SQL commands as user SYS.</Control_Description>
Prompt			<Control_Risk>As use of the INITJVMAUX package could allow an unauthorized user to run SQL commands as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'INITJVMAUX' REVOKE EXECUTE ON INITJVMAUX FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='INITJVMAUX';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='INITJVMAUX';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON INITJVMAUX FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'INITJVMAUX'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='INITJVMAUX';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>47</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:47</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'LTADM'</Control_Name>
Prompt			<Control_Description>The Oracle database LTADM package is shipped as undocumented and allows privilege escalation if granted to unprivileged users.</Control_Description>
Prompt			<Control_Risk>As use of the LTADM package could allow an unauthorized user to run any SQL command as user SYS.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'LTADM' REVOKE EXECUTE ON LTADM FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='LTADM';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='LTADM';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON LTADM FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'LTADM'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='LTADM';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>48</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:48</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_DBWS'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_DBWS package can be used to read/write file to web-based applications on the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_DBWS package could allow an unauthorized user to corrupt the HTTP stream used for carry the protocols that communicate with the instances web-based external communications, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_DBWS' REVOKE EXECUTE ON UTL_DBWS FROM 'PUBLIC'; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_DBWS';</Control_Parameter_1>
Prompt			<Control_Recommendation>To remediate this setting execute the following SQL statement. REVOKE EXECUTE ON UTL_DBWS FROM 'PUBLIC';</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_DBWS'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_DBWS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>49</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:49</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_FILE'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_FILE package can be used to read/write files located on the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_FILE package could allow an user to read files at the operating system. These files could contain sensitive information (e.g. passwords in .bash_history).</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_FILE' REVOKE EXECUTE ON UTL_FILE FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_FILE';</Control_Parameter_1>
Prompt			<Control_Recommendation>To remediate this setting execute the following SQL statement. REVOKE EXECUTE ON UTL_FILE FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_FILE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_FILE';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>50</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:50</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_HTTP'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_HTTP package can be used to perform HTTP-requests. This could be used to send information to the outside.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_HTTP package could be used to send (sensitive) information to external websites. The use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_HTTP' REVOKE EXECUTE ON UTL_HTTP FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_HTTP';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_HTTP';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON UTL_HTTP FROM PUBLIC</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_HTTP'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_HTTP';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>51</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:51</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_INADDR'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_INADDR package can be used to create specially crafted error messages or send information via DNS to the outside.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_INADDR package is often used in SQL Injection attacks from the web it should be revoked from public.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_INADDR' REVOKE EXECUTE ON UTL_INADDR FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_INADDR';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_INADDR';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON UTL_INADDR FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_INADDR'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_INADDR';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>52</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:52</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_MAIL'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_MAIL package can be used to send email from the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_MAIL package could allow an unauthorized user to corrupt the SMTP function to accept or generate junk mail that can result in a Denial-of-Service condition due to network saturation, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_MAIL' REVOKE EXECUTE ON UTL_MAIL FROM PUBLIC; </Agreed_Value>	
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_MAIL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_MAIL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON UTL_MAIL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_MAIL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_MAIL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>53</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:53</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_ORAMTS'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_ORAMTS package can be used to perform HTTP-requests. This could be used to send information to the outside.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_ORAMTS package could be used to send (sensitive) information to external websites. The use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_ORAMTS' REVOKE EXECUTE ON UTL_ORAMTS FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_ORAMTS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE'AND TABLE_NAME='UTL_ORAMTS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON UTL_ORAMTS FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_ORAMTS'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_ORAMTS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>54</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>4.1.18</CIS_Number>
Prompt			<Control_Name>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_SMTP'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_SMTP package can be used to send email from the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_SMTP package could allow an unauthorized user to corrupt the SMTP function to accept or generate junk mail that can result in a Denial-of-Service condition due to network saturation, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_SMTP' REVOKE EXECUTE ON UTL_SMTP FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_SMTP';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_SMTP';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON UTL_SMTP FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_SMTP'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_SMTP';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>55</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:55</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'UTL_TCP'</Control_Name>
Prompt			<Control_Description>The Oracle database UTL_TCP package can be used to read/write file to TCP sockets on the server where the Oracle instance is installed.</Control_Description>
Prompt			<Control_Risk>As use of the UTL_TCP package could allow an unauthorized user to corrupt the TCP stream used for carry the protocols that communicate with the instances external communications, use of this package should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'UTL_TCP' REVOKE EXECUTE ON UTL_TCP FROM PUBLIC; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_TCP';</Control_Parameter_1>
Prompt			<Control_Recommendation>To remediate this setting execute the following SQL statement. REVOKE EXECUTE ON UTL_TCP FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'UTL_TCP'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='UTL_TCP';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>56</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:56</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'WWV_DBMS_SQL'</Control_Name>
Prompt			<Control_Description>The Oracle database WWV_DBMS_SQL package is shipped as undocumented and allows Oracle Application Express to run dynamic SQL statements.</Control_Description>
Prompt			<Control_Risk>As use of the WWV_DBMS_SQL package could allow an unauthorized user to run SQL statements as Application Express (APEX) user.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'WWV_DBMS_SQL' REVOKE EXECUTE ON WWV_DBMS_SQL FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_DBMS_SQL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_DBMS_SQL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON WWV_DBMS_SQL FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'WWV_DBMS_SQL'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_DBMS_SQL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>57</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:57</CIS_Number>
Prompt			<Control_Name>EXECUTE Is Revoked from 'PUBLIC' on 'WWV_EXECUTE_IMMEDIATE'</Control_Name>
Prompt			<Control_Description>The Oracle database WWV_EXECUTE_IMMEDIATE package is shipped as undocumented and allows Oracle Application Express to run dynamic SQL statements.</Control_Description>
Prompt			<Control_Risk>As use of the WWV_EXECUTE_IMMEDIATE package could allow an unauthorized user to run SQL statements as Application Express (APEX) user.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE' Is Revoked from 'PUBLIC' on 'WWV_EXECUTE_IMMEDIATE' REVOKE EXECUTE ON WWV_EXECUTE_IMMEDIATE FROM PUBLIC;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_EXECUTE_IMMEDIATE';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_EXECUTE_IMMEDIATE';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE ON WWV_EXECUTE_IMMEDIATE FROM PUBLIC;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE Is not Revoked from 'PUBLIC' on 'WWV_EXECUTE_IMMEDIATE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE='PUBLIC' AND PRIVILEGE='EXECUTE' AND TABLE_NAME='WWV_EXECUTE_IMMEDIATE';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>58</S_No>
Prompt			<Category>Revoke Role Privileges</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:58</CIS_Number>
Prompt			<Control_Name>EXECUTE_CATALOG_ROLE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database EXECUTE_CATALOG_ROLE provides EXECUTE privileges for a number of packages and procedures in the data dictionary in the SYS schema.</Control_Description>
Prompt			<Control_Risk>As permitting unauthorized access to the EXECUTE_CATALOG_ROLE can allow the disruption of operations by initialization of rogue procedures, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXECUTE_CATALOG_ROLE' Is Revoked from Unauthorized 'GRANTEE' REVOKE EXECUTE_CATALOG_ROLE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='EXECUTE_CATALOG_ROLE' AND grantee not in ('DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='EXECUTE_CATALOG_ROLE' AND grantee not in ('DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXECUTE_CATALOG_ROLE FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXECUTE_CATALOG_ROLE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='EXECUTE_CATALOG_ROLE' AND grantee not in ('DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>59</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:59</CIS_Number>
Prompt			<Control_Name>EXEMPT ACCESS POLICY Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database EXEMPT ACCESS POLICY keyword provides the user the capability to access all the table rows regardless of row-level security lockouts.</Control_Description>
Prompt			<Control_Risk>As assignment of the EXEMPT ACCESS POLICY privilege can allow an unauthorized user to potentially access/change confidential data, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'EXEMPT ACCESS POLICY' Is Revoked from Unauthorized 'GRANTEE' REVOKE EXEMPT ACCESS POLICY FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXEMPT ACCESS POLICY';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXEMPT ACCESS POLICY';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE EXEMPT ACCESS POLICY FROM grantee</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when EXEMPT ACCESS POLICY Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='EXEMPT ACCESS POLICY';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>60</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:60</CIS_Number>
Prompt			<Control_Name>GRANT ANY OBJECT PRIVILEGE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database GRANT ANY OBJECT PRIVILEGE keyword provides the grantee the capability to grant access to any single or multiple combinations of objects to any grantee in the catalog of the database.</Control_Description>
Prompt			<Control_Risk>As authorization to use the GRANT ANY OBJECT PRIVILEGE capability can allow an unauthorized user to potentially access/change confidential data or damage the data catalog due to potential complete instance access, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT ANY OBJECT PRIVILEGE' Is Revoked from Unauthorized 'GRANTEE' REVOKE GRANT ANY OBJECT PRIVILEGE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE','EM_EXPRESS_ALL', 'DV_REALM_OWNER');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE GRANT ANY OBJECT PRIVILEGE FROM grantee;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt        <Comments>Control becomes NON-COMPLIANT when GRANT ANY OBJECT PRIVILEGE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE');
Prompt </Actual_Value>	
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>61</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:61</CIS_Number>
Prompt			<Control_Name>Ensure 'GRANT ANY PRIVILEGE' Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database GRANT ANY PRIVILEGE keyword provides the grantee the capability to grant any single privilege to any item in the catalog of the database.</Control_Description>
Prompt			<Control_Risk>As authorization to use the GRANT ANY PRIVILEGE capability can allow an unauthorized user to potentially access/change confidential data or damage the data catalog due to potential complete instance access, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT ANY PRIVILEGE' Is Revoked from Unauthorized 'GRANTEE' REVOKE GRANT ANY PRIVILEGE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt      SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND GRANTEE NOT IN ('DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE','DV_REALM_OWNER', 'EM_EXPRESS_ALL');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE GRANT ANY PRIVILEGE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when GRANT ANY PRIVILEGE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DBA','SYS','IMP_FULL_DATABASE','DATAPUMP_IMP_FULL_DATABASE');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>62</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:62</CIS_Number>
Prompt			<Control_Name>Ensure 'GRANT ANY ROLE' Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database GRANT ANY ROLE keyword provides the grantee the capability to grant any single role to any grantee in the catalog of the database.</Control_Description>
Prompt			<Control_Risk>As authorization to use the GRANT ANY ROLE capability can allow an unauthorized user to potentially access/change confidential data or damage the data catalog due to potential complete instance access, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT ANY ROLE' Is Revoked from Unauthorized 'GRANTEE' REVOKE GRANT ANY ROLE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY ROLE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DV_OWNER', 'GSMADMIN_INTERNAL', 'DBA','SYS','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE', 'SPATIAL_WFS_ADMIN_USR','SPATIAL_CSW_ADMIN_USR');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY ROLE' AND GRANTEE NOT IN ('DBA','SYS','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE','SPATIAL_WFS_ADMIN_USR','SPATIAL_CSW_ADMIN_USR', 'GSMADMIN_INTERNAL','DV_REALM_OWNER', 'EM_EXPRESS_ALL', 'DV_OWNER');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE GRANT ANY ROLE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when GRANT ANY ROLE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='GRANT ANY ROLE' AND GRANTEE NOT IN ('EM_EXPRESS_ALL', 'DV_REALM_OWNER', 'DV_OWNER', 'GSMADMIN_INTERNAL', 'DBA','SYS','DATAPUMP_IMP_FULL_DATABASE','IMP_FULL_DATABASE', 'SPATIAL_WFS_ADMIN_USR','SPATIAL_CSW_ADMIN_USR');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>63</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:63</CIS_Number>
Prompt			<Control_Name>Proxy Users Have Only 'CONNECT' Privilege</Control_Name>
Prompt			<Control_Description>Do not grant privileges directly to proxy users</Control_Description>
Prompt			<Control_Risk>A proxy user should only have the ability to connect to the database.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure Proxy Users Have Only 'CONNECT' Privilege REVOKE [PRIVILEGE] FROM [proxy_user];</Agreed_Value>
Prompt			<Control_Parameter_1>To assess this recommendation execute the following SQL statement. SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTEE IN ( SELECT PROXY FROM DBA_PROXIES ) AND GRANTED_ROLE NOT IN ('CONNECT');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT GRANTEE,GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTEE IN (SELECT PROXY FROM DBA_PROXIES) AND GRANTED_ROLE NOT IN ('CONNECT') UNION
Prompt SELECT GRANTEE,PRIVILEGE FROM DBA_SYS_PRIVS WHERE GRANTEE IN (SELECT PROXY FROM DBA_PROXIES) AND PRIVILEGE NOT IN ('CREATE SESSION') UNION
Prompt SELECT GRANTEE,PRIVILEGE FROM DBA_TAB_PRIVS WHERE GRANTEE IN (SELECT PROXY FROM DBA_PROXIES);
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE [PRIVILEGE] FROM [proxy_user];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Proxy users have additional privileges including "CONNECT" privilege.</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE GRANTEE IN ( SELECT PROXY FROM DBA_PROXIES ) AND GRANTED_ROLE NOT IN ('CONNECT');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>64</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:64</CIS_Number>
Prompt			<Control_Name>SELECT ANY TABLE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database SELECT ANY TABLE privilege allows the designated user to open any table, except of SYS, to view it.</Control_Description>
Prompt			<Control_Risk>As assignment of the SELECT ANY TABLE privilege can allow the unauthorized viewing of sensitive data, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SELECT ANY TABLE' Is Revoked from Unauthorized 'GRANTEE' REVOKE SELECT ANY TABLE FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY TABLE' AND GRANTEE NOT IN ('DV_REALM_OWNER','DBA', 'MDSYS', 'SYS', 'IMP_FULL_DATABASE', 'EXP_FULL_DATABASE', 'DATAPUMP_IMP_FULL_DATABASE', 'WMSYS', 'SYSTEM', 'OLAP_DBA', 'OLAPSYS');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY TABLE' AND GRANTEE NOT IN ('DBA', 'MDSYS', 'SYS', 'IMP_FULL_DATABASE', 'EXP_FULL_DATABASE', 'DATAPUMP_IMP_FULL_DATABASE', 'WMSYS', 'SYSTEM','OLAP_DBA', 'DV_REALM_OWNER');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt REVOKE SELECT ANY TABLE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SELECT ANY TABLE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY TABLE' AND GRANTEE NOT IN ('DV_REALM_OWNER','DBA', 'MDSYS', 'SYS', 'IMP_FULL_DATABASE', 'EXP_FULL_DATABASE', 'DATAPUMP_IMP_FULL_DATABASE', 'WMSYS', 'SYSTEM', 'OLAP_DBA', 'OLAPSYS');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>65</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:65</CIS_Number>
Prompt			<Control_Name>SELECT_ANY_DICTIONARY Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database SELECT ANY DICTIONARY privilege allows the designated user to access SYS schema objects.</Control_Description>
Prompt			<Control_Risk>The Oracle database SELECT ANY DICTIONARY privilege allows the designated user to access SYS schema objects. The Oracle password hashes are part of the SYS schema and can be selected using SELECT ANY DICTIONARY privileges.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SELECT_ANY_DICTIONARY' Is Revoked from Unauthorized 'GRANTEE' REVOKE SELECT_ANY_DICTIONARY FROM [grantee];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY DICTIONARY' AND GRANTEE NOT IN ('SYSBACKUP','SYSDG','DBA','DBSNMP','OEM_MONITOR', 'OLAPSYS','ORACLE_OCM','SYSMAN','WMSYS');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY DICTIONARY' AND GRANTEE NOT IN ('DBA','DBSNMP','OEM_MONITOR', 'OLAPSYS','ORACLE_OCM','SYSMAN','WMSYS','SYSBACKUP','SYSDG');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE SELECT_ANY_DICTIONARY FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SELECT_ANY_DICTIONARY Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, PRIVILEGE FROM DBA_SYS_PRIVS WHERE PRIVILEGE='SELECT ANY DICTIONARY' AND GRANTEE NOT IN ('SYSBACKUP','SYSDG','DBA','DBSNMP','OEM_MONITOR', 'OLAPSYS','ORACLE_OCM','SYSMAN','WMSYS');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>66</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:1:66</CIS_Number>
Prompt			<Control_Name>SELECT_CATALOG_ROLE Is Revoked from Unauthorized 'GRANTEE'</Control_Name>
Prompt			<Control_Description>The Oracle database SELECT_CATALOG_ROLE provides SELECT privileges on all data dictionary views held in the SYS schema.</Control_Description>
Prompt			<Control_Risk>As permitting unauthorized access to the SELECT_CATALOG_ROLE can allow the disclosure of all dictionary data, this capability should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SELECT_CATALOG_ROLE' Is Revoked from Unauthorized 'GRANTEE' REVOKE SELECT_CATALOG_ROLE FROM [grantee];
Prompt </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='SELECT_CATALOG_ROLE' AND grantee not in ('EM_EXPRESS_BASIC', 'SYSBACKUP', 'DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE','OEM_MONITOR');</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='SELECT_CATALOG_ROLE' AND grantee not in ('DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE','OEM_MONITOR', 'SYSBACKUP','EM_EXPRESS_BASIC','SYSMAN');
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # REVOKE SELECT_CATALOG_ROLE FROM [grantee];</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when SELECT_CATALOG_ROLE Is not Revoked from Unauthorized 'GRANTEE'</Comments>
Prompt <Actual_Value>
SELECT GRANTEE, GRANTED_ROLE FROM DBA_ROLE_PRIVS WHERE granted_role='SELECT_CATALOG_ROLE' AND grantee not in ('EM_EXPRESS_BASIC', 'SYSBACKUP', 'DBA','SYS','IMP_FULL_DATABASE','EXP_FULL_DATABASE','OEM_MONITOR');
Prompt </Actual_Value>	
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>67</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:1:67</CIS_Number>
Prompt			<Control_Name>SESSIONS_PER_USER Is Less than or Equal to '10'</Control_Name>
Prompt			<Control_Description>The SESSIONS_PER_USER (Number of sessions allowed) determines the maximum number of user sessions that are allowed	to be open concurrently</Control_Description>
Prompt			<Control_Risk>As limiting the number of	the	SESSIONS_PER_USER can help prevent memory resource exhaustion by poorly	formed requests	or intentional Denial-of-Service attacks,	this value should be set according to the needs	of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SESSIONS_PER_USER' Is Less than or Equal to '10' ALTER PROFILE [profile_name] LIMIT SESSIONS_PER_USER 10;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='SESSIONS_PER_USER' AND  ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 10 ); </Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='SESSIONS_PER_USER' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 10 );
Prompt 2. To remediate this setting execute the following SQL statement for each PROFILE returned by the audit procedure.
Prompt # ALTER PROFILE profile_name LIMIT SESSIONS_PER_USER 10;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SESSIONS_PER_USER Is not less than or Equal to '10'</Comments>      
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='SESSIONS_PER_USER' AND  ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 10 ); 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>68</S_No>
Prompt			<Category>Authentication and Authorization</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>4.5.7</CIS_Number>
Prompt			<Control_Name>SYS.USER$MIG Has Been Dropped</Control_Name>
Prompt			<Control_Description>The table sys.user$mig is created during migration and contains the Oracle password hashes before the migration starts.</Control_Description>
Prompt			<Control_Risk>The table sys.user$mig is not deleted after the migration. An attacker could access the table containing the Oracle password hashes.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SYS.USER$MIG' should Been Dropped DROP TABLE SYS.USER$MIG;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT OWNER, TABLE_NAME FROM ALL_TABLES WHERE OWNER='SYS' AND TABLE_NAME='USER$MIG';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To check execute the following SQL statement: SELECT OWNER, TABLE_NAME FROM ALL_TABLES WHERE OWNER='SYS' AND TABLE_NAME='USER$MIG'; Lack of results implies compliance.
Prompt 2. To remediate this setting execute the following SQL statement:
Prompt # DROP TABLE SYS.USER$MIG;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SYS.USER$MIG has not Been Dropped</Comments>
Prompt <Actual_Value>
SELECT OWNER, TABLE_NAME FROM ALL_TABLES WHERE OWNER='SYS' AND TABLE_NAME='USER$MIG';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>69</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:1</CIS_Number>
Prompt			<Control_Name>Set Audit Option ALL on 'SYS.AUD$'</Control_Name>
Prompt			<Control_Description>The logging of attempts to alter the audit trail in the SYS.AUD$ table (open for read/update/delete/view) will provide a record of any activities that may indicate unauthorized attempts to access the audit trail. Rationale: As</Control_Description>
Prompt			<Control_Risk>As the logging of attempts to alter the SYS.AUD$ table can provide forensic evidence of the initiation of a pattern of unauthorized activities, this logging capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Enable 'ALL' Audit Option on 'SYS.AUD$' AUDIT ALL ON SYS.AUD$ BY ACCESS;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT * FROM DBA_OBJ_AUDIT_OPTS WHERE OBJECT_NAME='AUD$' AND ALT='A/A' AND AUD='A/A' AND COM='A/A' AND DEL='A/A' AND GRA='A/A' AND IND='A/A' AND INS='A/A' AND LOC='A/A' AND REN='A/A' AND SEL='A/A' AND UPD='A/A' AND FBK='A/A';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT * FROM DBA_OBJ_AUDIT_OPTS WHERE OBJECT_NAME='AUD$' AND ALT='A/A' AND AUD='A/A' AND COM='A/A' AND DEL='A/A' AND GRA='A/A' AND IND='A/A' AND INS='A/A' AND LOC='A/A' AND REN='A/A' AND SEL='A/A' AND UPD='A/A' AND FBK='A/A';
Prompt 2. Execute the following SQL statement to remediate this setting:
Prompt # AUDIT ALL ON SYS.AUD$ BY ACCESS;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option all has not been set on 'SYS.AUD$'</Comments>
Prompt <Actual_Value>
SELECT * FROM DBA_OBJ_AUDIT_OPTS WHERE OBJECT_NAME='AUD$' AND ALT='A/A' AND AUD='A/A' AND COM='A/A' AND DEL='A/A' AND GRA='A/A' AND IND='A/A' AND INS='A/A' AND LOC='A/A' AND REN='A/A' AND SEL='A/A' AND UPD='A/A' AND FBK='A/A';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>70</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:2</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'ALTER PROFILE'</Control_Name>
Prompt			<Control_Description>The PROFILE object allows for the creation of a set of database resource limits that can be assigned to a user, so that that user cannot exceed those resource limitations.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation, alteration, or dropping of a PROFILE can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALTER PROFILE' Audit Option should be enabled AUDIT ALTER PROFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT ALTER PROFILE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set on 'ALTER PROFILE'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>71</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:3</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'ALTER SYSTEM'</Control_Name>
Prompt			<Control_Description>This will audit all attempts to ALTER SYSTEM, whether successful or not and regardless of whether or not the ALTER SYSTEM privilege is held by the user attempting the action.</Control_Description>
Prompt			<Control_Risk>Alter system allows one to change instance settings, including security settings and auditing options. Additionally alter system can be used to run operating system commands using undocumented Oracle functionality. Any unauthorized attempt to alter the system should be cause for concern. Alterations outside of some specified maintenance window may be of concern. In forensics, these audit records could be quite useful.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALTER SYSTEM' Audit Option should be enabled AUDIT ALTER SYSTEM;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER SYSTEM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER SYSTEM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT ALTER SYSTEM;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set on 'ALTER SYSTEM'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER SYSTEM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>72</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:4</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'ALTER USER'</Control_Name>
Prompt			<Control_Description>The USER object for the Oracle database is a specification of an object which is an account through which either a human or an application can connect to, via a JDBC or log into, via a CLI, and interact with the database instance according to the roles and privileges allotted to account.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation, alteration, or dropping of a USER can provide forensic evidence about a pattern of suspect/unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ALTER USER' Audit Option should be enabled AUDIT ALTER USER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT ALTER USER;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option has not been set on 'ALTER USER'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ALTER USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>73</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:5</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'DATABASE LINK'</Control_Name>
Prompt			<Control_Description>All activities on database links should be audited.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation or dropping of a DATABASE LINK can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DATABASE LINK' Audit Option should be enabled AUDIT DATABASE LINK;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DATABASE LINK' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>Execute the following SQL statement to remediate this setting. AUDIT DATABASE LINK;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option has not been set on 'DATABASE LINK'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DATABASE LINK' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>74</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:6</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'DROP ANY PROCEDURE'</Control_Name>
Prompt			<Control_Description>The AUDIT DROP ANY PROCEDURE command is auditing the creation of procedures in other schema.</Control_Description>
Prompt			<Control_Risk>Dropping procedures of another user could be part of an privilege escalation exploit and should be audited.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DROP ANY PROCEDURE' Audit Option should be enabled AUDIT DROP ANY PROCEDURE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP ANY PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP ANY PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT DROP ANY PROCEDURE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option has not been set to 'DROP ANY PROCEDURE'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP ANY PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>75</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:7</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'DROP PROFILE'</Control_Name>
Prompt			<Control_Description>The PROFILE object allows for the creation of a set of database resource limits that can be assigned to a user, so that that user cannot exceed those resource limitations.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation, alteration, or dropping of a PROFILE can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DROP PROFILE' Audit Option should be enabled AUDIT DROP PROFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT DROP PROFILE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'DROP PROFILE'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>76</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:8</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'DROP USER'</Control_Name>
Prompt			<Control_Description>The PROFILE object allows for the creation of a set of database resource limits that can be assigned to a user, so that that user cannot exceed those resource limitations.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation, alteration, or dropping of a PROFILE can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DROP USER' Audit Option should be enabled AUDIT DROP USER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT DROP USER;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'DROP USER'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>77</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:9</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'GRANT ANY OBJECT PRIVILEGE'</Control_Name>
Prompt			<Control_Description>GRANT ANY OBJECT PRIVILEGE allows the user to grant or revoke any object privilege, which includes privileges on tables, directories, mining models, etc. This audits all uses of that privilege.</Control_Description>
Prompt			<Control_Risk>Logging of privilege grants that can lead to the creation, alteration, or deletion of critical data, the modification of objects, object privilege propagation and other such activities can be critical to forensic investigations.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT ANY OBJECT PRIVILEGE' Audit Option should be enabled AUDIT GRANT ANY OBJECT PRIVILEGE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT GRANT ANY OBJECT PRIVILEGE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'GRANT ANY OBJECT PRIVILEGE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY OBJECT PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>78</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:10</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'GRANT ANY PRIVILEGE'</Control_Name>
Prompt			<Control_Description>This audits all uses of the system privilege named GRANT ANY PRIVILEGE. Actions by users not holding this privilege are not audited.</Control_Description>
Prompt			<Control_Risk>GRANT ANY PRIVILEGE allows a user to grant any system privilege, including the most powerful privileges typically available only to administrators - to change the security infrastructure, to drop/add/modify users and more. Auditing the use of this privilege is part of a comprehensive auditing policy that can help in detecting issues and can be useful in forensics.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT ANY PRIVILEGE' Audit Option should be enabled AUDIT GRANT ANY PRIVILEGE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS'   AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT GRANT ANY PRIVILEGE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'GRANT ANY PRIVILEGE'</Comments>
Prompt <Actual_Value>
SELECT PRIVILEGE, SUCCESS, FAILURE FROM DBA_PRIV_AUDIT_OPTS WHERE PRIVILEGE='GRANT ANY PRIVILEGE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>79</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:11</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'GRANT DIRECTORY'</Control_Name>
Prompt			<Control_Description>The DIRECTORY object allows for the creation of a directory object that specifies an alias for a directory on the server file system, where the external binary file LOBs (BFILEs)/ table data are located.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation or dropping of a DIRECTORY can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'GRANT DIRECTORY' Audit Option should be enabled AUDIT GRANT DIRECTORY;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='GRANT DIRECTORY' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='GRANT DIRECTORY' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT GRANT DIRECTORY;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'GRANT DIRECTORY'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='GRANT DIRECTORY' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>80</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:12</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'PROCEDURE'</Control_Name>
Prompt			<Control_Description>In this statement audit, "PROCEDURE" means any procedure, function, package or library. Any attempt, successful or not, to create or drop any of these types of objects is audited, regardless of privilege or lack thereof. Java schema objects (sources, classes, and resources) are considered the same as procedures for purposes of auditing SQL statements.</Control_Description>
Prompt			<Control_Risk>Any unauthorized attempts to create or drop a procedure in anothers schema should cause concern, whether successful or not. Changes to critical store code can dramatically change the behavior of the application and produce serious security consequences, including privilege escalation and introducing SQL injection vulnerabilities. Audit records of such changes can be helpful in forensics.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'PROCEDURE' Audit Option should be enabled AUDIT PROCEDURE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT PROCEDURE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'PROCEDURE'</Comments>

Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROCEDURE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>81</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:13</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'PROFILE'</Control_Name>
Prompt			<Control_Description>The PROFILE object allows for the creation of a set of database resource limits that can be assigned to a user, so that that user cannot exceed those resource limitations. This will audit all attempts, successful or not, to create, drop or alter any profile.</Control_Description>
Prompt			<Control_Risk>As profiles are part of the database security infrastructure, auditing the modification of profiles is recommended.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'PROFILE' Audit Option should be enabled AUDIT PROFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT PROFILE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'PROFILE'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PROFILE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>82</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>5.10</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'PUBLIC DATABASE LINK'</Control_Name>
Prompt			<Control_Description>The PUBLIC DATABASE LINK object allows for the creation of a public link for an application-based "user" to access the database for connections/session creation</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation, alteration, or dropping of a PUBLIC DATABASE LINK can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'PUBLIC DATABASE LINK' Audit Option should be enabled AUDIT PUBLIC DATABASE LINK;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC DATABASE LINK' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC DATABASE LINK' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT PUBLIC DATABASE LINK;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'PUBLIC DATABASE LINK'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC DATABASE LINK' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>83</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:15</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'PUBLIC SYNONYM'</Control_Name>
Prompt			<Control_Description>The PUBLIC SYNONYM object allows for the creation of an alternate description of an object and public synonyms are accessible by all users that have the appropriate privileges to the underlying object.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation or dropping of a PUBLIC SYNONYM can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'PUBLIC SYNONYM' Audit Option should be enabled AUDIT PUBLIC SYNONYM;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT PUBLIC SYNONYM;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'PUBLIC SYNONYM'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='PUBLIC SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>84</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:16</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'ROLE'</Control_Name>
Prompt			<Control_Description>The ROLE object allows for the creation of a set of privileges that can be granted to users or other roles. This audits all attempts, successful or not, to create, drop, alter or set roles.</Control_Description>
Prompt			<Control_Risk>Roles are a key database security infrastructure component. Any attempt to create, drop or alter a role should be audited. This statement auditing option also audits attempts, successful or not, to set a role in a session. Any unauthorized attempts to create, drop or alter a role may be worthy of investigation. Attempts to set a role by users without the role privilege may warrant investigation.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'ROLE' Audit Option should be enabled AUDIT ROLE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ROLE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ROLE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT ROLE;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'ROLE'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='ROLE' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>85</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:17</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'SELECT ANY DICTIONARY'</Control_Name>
Prompt			<Control_Description>The SELECT ANY DICTIONARY capability allows the user to view the definitions of all schema objects in the database.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the capability to access the description of all schema objects in the database can provide forensic evidence about a pattern of unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SELECT ANY DICTIONARY' Audit Option should be enabled AUDIT SELECT ANY DICTIONARY;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE  FROM DBA_STMT_AUDIT_OPTS  WHERE AUDIT_OPTION='SELECT ANY DICTIONARY' AND USER_NAME IS NULL  AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SELECT ANY DICTIONARY' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT SELECT ANY DICTIONARY;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'SELECT ANY DICTIONARY'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE  FROM DBA_STMT_AUDIT_OPTS  WHERE AUDIT_OPTION='SELECT ANY DICTIONARY' AND USER_NAME IS NULL  AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>86</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:18</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'SYNONYM'</Control_Name>
Prompt			<Control_Description>The SYNONYM operation allows for the creation of a an alternative name for a database object such as a Java class schema object, materialized view, operator, package, procedure, sequence, stored function, table, view, user-defined object type, even another synonym; this synonym puts a dependency on its target and is rendered invalid if the target object is changed/dropped.</Control_Description>
Prompt			<Control_Risk>As the logging of user activities involving the creation or dropping of a SYNONYM can provide forensic evidence about a pattern of suspect/unauthorized activities, the audit capability should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SYNONYM' Audit Option should be enabled AUDIT SYNONYM;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT SYNONYM;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'SYNONYM'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYNONYM' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>87</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:19</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'SYSTEM GRANT'</Control_Name>
Prompt			<Control_Description>This will audit any attempt, successful or not, to grant or revoke any system privilege or role - regardless of privilege held by the user attempting the operation.</Control_Description>
Prompt			<Control_Risk>Logging of all grant and revokes (roles and system privileges) can provide forensic evidence about a pattern of suspect/unauthorized activities. Any unauthorized attempt may be cause for further investigation.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'SYSTEM GRANT' Audit Option should be enabled AUDIT SYSTEM GRANT;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYSTEM GRANT' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYSTEM GRANT' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT SYSTEM GRANT;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'SYSTEM GRANT'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='SYSTEM GRANT' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>88</S_No>
Prompt			<Category>Audit</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:20</CIS_Number>
Prompt			<Control_Name>Set Audit Option to 'TRIGGER'</Control_Name>
Prompt			<Control_Description>A TRIGGER may be used to modify DML actions or invoke other (recursive) actions when some types of user-initiated actions occur. This will audit any attempt, successful or not, to create, drop, enable or disable any schema trigger in any schema regardless of privilege or lack thereof. For enabling and disabling a trigger, it covers both alter trigger and alter table.</Control_Description>
Prompt			<Control_Risk>Triggers are often part of schema security, data validation and other critical constraints upon actions and data. A trigger in another schema may be used to escalate privileges, redirect operations, transform data and perform other sorts of perhaps undesired actions. Any unauthorized attempt to create, drop or alter a trigger in another schema may be cause for investigation.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt           <Agreed_Value>Ensure 'TRIGGER' Audit Option should be enabled AUDIT TRIGGER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='TRIGGER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation execute the following SQL statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='TRIGGER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT TRIGGER;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'TRIGGER'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='TRIGGER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>89</S_No>
Prompt			<Category>Logging</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:2:21</CIS_Number>
Prompt			<Control_Name>Set Audit Option to USER </Control_Name>
Prompt			<Control_Description>The USER object in the Oracle database an account through which a connection may be made to interact with the database according to the roles and privileges allotted to account. It is also a schema with may own database objects. This audits all activities and  requests to create, drop or alter a user, including a user changing their own password. (The latter is not audited by ‘audit ALTER USER’.)</Control_Description>
Prompt			<Control_Risk>Any unauthorized attempts to create, drop or alter a user should cause concern, whether successful or not. It can also be useful in forensics if an account is compromised and is mandated by many common security initiatives. An abnormally high number of these activities in a given period might be worth investigation. Any failed attempt to drop a user or create a user may be worth further review.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'USER' Audit Option should be enabled AUDIT USER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS'</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL Statement.
Prompt SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt 2. Execute the following SQL statement to remediate this setting: 
Prompt # AUDIT USER;</Control_Recommendation>
Prompt			<Operation>NOTEQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when Audit Option  has not been set to 'USER'</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies a finding.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>90</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:1</CIS_Number>
Prompt			<Control_Name>All Default Passwords Are Changed</Control_Name>
Prompt			<Control_Description>The Oracle installation has a view called DBA_USERS_WITH_DEFPWD, which keeps a list of all database users making use of default passwords.</Control_Description>
Prompt			<Control_Risk>Default passwords should be considered "well known" to attackers. Consequently, if default passwords remain in place any attacker with access to the database then has the ability to authenticate as the user with that default password. When default passwords are altered, this circumstance is mitigated.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the following SQL statement for each USERNAME returned in the Audit Procedure PASSWORD [username]</Agreed_Value>	
Prompt			<Control_Parameter_1>SELECT USERNAME FROM DBA_USERS_WITH_DEFPWD WHERE USERNAME NOT LIKE '%XS$NULL%';</Control_Parameter_1>
Prompt			<Control_Recommendation>To remediate this recommendation, you may perform either of the following actions:1. Manually issue the following SQL statement for each USERNAME returned in theAudit Procedure:PASSWORD [username]
Prompt 2. Execute the following SQL script to randomly assign passwords: begin for r_user in (select username from dba_users_with_defpwd where username not like '%XS$NULL%') loop DBMS_OUTPUT.PUT_LINE('Password for user '||r_user.username||' will be changed.'); execute immediate 'alter user "'||r_user.username||'" identified by "'||DBMS_RANDOM.string('a',16)||'"account lock password expire'; end loop;end;
Prompt / /</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when All Default Passwords Are not Changed</Comments>
Prompt <Actual_Value>
SELECT USERNAME FROM DBA_USERS_WITH_DEFPWD WHERE USERNAME NOT LIKE '%XS$NULL%';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>The assessment fails if results are returned</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>91</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:2</CIS_Number>
Prompt			<Control_Name>DBA_USERS.PASSWORD</Control_Name>
Prompt			<Control_Description>The password='EXTERNAL' setting determines whether or not a user can be authenticated by a remote OS to allow access to the database with full authorization.</Control_Description>
Prompt			<Control_Risk>As allowing remote OS authentication of a user to the database can potentially allow supposed "privileged users" to connect as "authenticated," even when the remote system is compromised, these logins should be disabled/restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure 'DBA_USERS.PASSWORD' Is Not Set to 'EXTERNAL' for Any User ALTER USER [username] IDENTIFIED BY [password];</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT USERNAME FROM DBA_USERS WHERE PASSWORD='EXTERNAL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT USERNAME FROM DBA_USERS WHERE PASSWORD='EXTERNAL';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER USER username IDENTIFIED BY password;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when DBA_USERS.PASSWORD is set to 'EXTERNAL'</Comments>
Prompt <Actual_Value>
SELECT USERNAME FROM DBA_USERS WHERE PASSWORD='EXTERNAL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>92</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:3:3</CIS_Number>
Prompt			<Control_Name>FAILED_LOGIN_ATTEMPTS</Control_Name>
Prompt			<Control_Description>The failed_login_attempts setting determines how many failed login attempts are permitted before the system locks the users account. While different profiles can have different and more restrictive settings, such as USERS and APPS, the minimum(s) recommended here should be set on the DEFAULT profile.</Control_Description>
Prompt			<Control_Risk>As repeated failed login attempts can indicate the initiation of a brute-force login attack, this value should be set according to the needs of the organization (see warning below on a known bug that can make this security measure backfire).</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure FAILED_LOGIN_ATTEMPTS should be set to 3;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='FAILED_LOGIN_ATTEMPTS' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 3 );</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='FAILED_LOGIN_ATTEMPTS' AND (LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 3 );
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER PROFILE profile_name LIMIT FAILED_LOGIN_ATTEMPTS 3;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when FAILED_LOGIN_ATTEMPTS limit is not set to 3</Comments>

Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='FAILED_LOGIN_ATTEMPTS' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT >= 3 );
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>93</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:4</CIS_Number>
Prompt			<Control_Name>PASSWORD_GRACE_TIME</Control_Name>
Prompt			<Control_Description>The password_grace_time setting determines how many days can pass after the user's password expires before the user's login capability is automatically locked out.</Control_Description>
Prompt			<Control_Risk>As locking the user account after the expiration of the password change requirements grace period can help prevent password-based attack against a forgotten or disused accounts, while still allowing the account and its information to be accessible by DBA intervention, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure PASSWORD_GRACE_TIME should be Less than or Equal to '3';</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_GRACE_TIME' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT gt 3 );</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_GRACE_TIME' AND (LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 3);
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER PROFILE DEFAULT LIMIT PASSWORD_GRACE_TIME 3;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when PASSWORD_GRACE_TIME limit is not set to 3</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_GRACE_TIME' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 3 );
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>94</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:5</CIS_Number>
Prompt			<Control_Name>PASSWORD_LIFE_TIME</Control_Name>
Prompt			<Control_Description>The password_life_time setting determines how long a password may be used before the user is required to be change it.</Control_Description>
Prompt			<Control_Risk>As allowing passwords to remain unchanged for long periods makes the success of brute- force login attacks more likely, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure PASSWORD_LIFE_TIME should be less than or equal to 60;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LIFE_TIME' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT gt 90 );</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LIFE_TIME' AND (LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 60);
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER PROFILE profile_name LIMIT PASSWORD_LIFE_TIME 60;;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when PASSWORD_LIFE_TIME limit is not set to 60</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LIFE_TIME' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT > 90 );
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>95</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:6</CIS_Number>
Prompt			<Control_Name>PASSWORD_LOCK_TIME</Control_Name>
Prompt			<Control_Description>The PASSWORD_LOCK_TIME setting determines how many days must pass for the users account to be unlocked after the set number of failed login attempts has occurred.</Control_Description>
Prompt			<Control_Risk>As locking the user account after repeated failed login attempts can block further brute- force login attacks, but can create administrative headaches as this account unlocking process always requires DBA intervention, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure PASSWORD_LOCK_TIME should be greater than or equal to '1'</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LOCK_TIME' AND ( LIMIT = Prompt 'DEFAULT'Prompt         OR LIMIT = 'UNLIMITED' OR LIMIT (less than or equal to) 1 );</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LOCK_TIME' AND (LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT (less than or equal to) 1
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt ALTER PROFILE profile_name LIMIT PASSWORD_LOCK_TIME 1;;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when PASSWORD_LOCK_TIME limit is not set to 1</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_LOCK_TIME' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT <= 1 );
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>96</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:7</CIS_Number>
Prompt			<Control_Name>PASSWORD_REUSE_MAX</Control_Name>
Prompt			<Control_Description>The password_reuse_max setting determines how many different passwords must be used before the user is allowed to reuse a prior password.</Control_Description>
Prompt			<Control_Risk>As allowing reuse of a password within a short period of time after the passwords initial use can make the success of both social-engineering and brute-force password-based attacks more likely, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure PASSWORD_REUSE_MAX should be less than or equal to 20;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_REUSE_MAX' AND ( LIMIT = 'DEFAULT' OR Prompt LIMIT = 'UNLIMITED' OR LIMIT (less than) 20 );</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_REUSE_MAX' AND (LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT (less than) 20);
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt ALTER PROFILE profile_name LIMIT PASSWORD_REUSE_MAX20;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when PASSWORD_REUSE_MAX is not less than or equal to 20</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_REUSE_MAX' AND ( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT < 20 );
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>97</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:8</CIS_Number>
Prompt			<Control_Name>PASSWORD_REUSE_TIME</Control_Name>
Prompt			<Control_Description>The password_reuse_time setting determines the amount of time in days that must pass before the same password may be reused.</Control_Description>
Prompt			<Control_Risk>As reusing the same password after only a short period of time has passed makes the success of brute-force login attacks more likely, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure PASSWORD_REUSE_TIME should be Greater than or Equal to 365</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME, LIMIT FROM (SELECT DISTINCT P.NAME "PROFILE", R.NAME "RESOURCE_NAME", TO_CHAR(DECODE(LIMIT#,0,(SELECT LIMIT# FROM PROFILE$ WHERE PROFILE#=0 AND RESOURCE#=2 AND TYPE#=1),LIMIT#)/86400) "LIMIT" FROM PROFNAME$ P, RESOURCE_MAP R, PROFILE$ L WHERE L.PROFILE# = P.PROFILE# AND L.RESOURCE# = R.RESOURCE# AND R.RESOURCE#=2 AND R.TYPE#=1) WHERE LIMIT lessthan 365;</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_REUSE_TIME' AND( LIMIT = 'DEFAULT' OR LIMIT = 'UNLIMITED' OR LIMIT (less than) 365);
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER PROFILE profile_name LIMIT PASSWORD_REUSE_TIME 365;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when PASSWORD_REUSE_TIME is not Greater than or equal to 365</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME, LIMIT FROM (SELECT DISTINCT P.NAME "PROFILE", R.NAME "RESOURCE_NAME", TO_CHAR(DECODE(LIMIT#,0,(SELECT LIMIT# FROM PROFILE$ WHERE PROFILE#=0 AND RESOURCE#=2 AND TYPE#=1),LIMIT#)/86400) "LIMIT" FROM PROFNAME$ P, RESOURCE_MAP R, PROFILE$ L WHERE L.PROFILE# = P.PROFILE# AND L.RESOURCE# = R.RESOURCE# AND R.RESOURCE#=2 AND R.TYPE#=1) WHERE LIMIT < 365;
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>98</S_No>
Prompt			<Category>Oracle-12C:3:9</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:3:9</CIS_Number>
Prompt			<Control_Name>PASSWORD_VERIFY_FUNCTION should be set for All Profiles</Control_Name>
Prompt			<Control_Description>The password_verify_function determines password settings requirements when a user password is changed at the SQL command prompt. This setting does not apply for users managed by the Oracle password file.</Control_Description>
Prompt			<Control_Risk>As requiring users to apply the 12cr2 security features in password creation, such as forcing mixed-case complexity, the blocking of simple combinations, and change/history settings can potentially thwart logins by unauthorized users, this function should be applied/enabled according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure to create a custom password verification function which fulfills the password requirements of the organization.</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT PROFILE, RESOURCE_NAME FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_VERIFY_FUNCTION' AND (LIMIT = 'DEFAULT' OR LIMIT = 'NULL');</Control_Parameter_1>
Prompt			<Control_Recommendation>To set the password_verify_function setting for database profiles to Password Verification Function 1. Use Prompt the utlpwdmg.sql file located at Oracle_home\RDBMS\Admin folder (if the file is not here, search for the file on the Oracle server) to create Prompt a function [verify_function] which would check for the following password attributes with defined values:
Prompt PASSWORD_GRACE_TIME 3 
Prompt PASSWORD_REUSE_TIME 365 
Prompt PASSWORD_REUSE_MAX 20 
Prompt FAILED_LOGIN_ATTEMPTS 3 
Prompt PASSWORD_LOCK_TIME 1 
Prompt Modify the line: If length(password) lt 4 by changing the minimum password length to 8. Function can be created by: Create or Replace Function Prompt [verify_function]
Prompt 2. Create [verify_function] from utlpwdmg.sql with the required password policy.
Prompt 3. From DBA_PROFILES, get the number of profiles present by using the following query:
Prompt # SELECT PROFILE, RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_VERIFY_FUNCTION';
Prompt 4. For these profiles, associate the function [verify_function] by using the following query: # ALTER PROFILE [profile name] LIMIT password_verify_function [verify_function]
Prompt 5. The password policy stated by function now would be applicable to all profiles. Reassociate or modify the users associated with profile/s value, for which password policy is modified (if modified). Execute the following SQL query:# ALTER USER [username] PROFILE [profile name].</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when PASSWORD_VERIFY_FUNCTION has not been set for All Profiles</Comments>
Prompt <Actual_Value>
SELECT PROFILE, RESOURCE_NAME FROM DBA_PROFILES WHERE RESOURCE_NAME='PASSWORD_VERIFY_FUNCTION' AND (LIMIT = 'DEFAULT' OR LIMIT = 'NULL');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Lack of results implies compliance</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>99</S_No>
Prompt			<Category>Password Requirements</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:4:9</CIS_Number>
Prompt			<Control_Name>REMOTE_LOGIN_PASSWORDFILE</Control_Name>
Prompt			<Control_Description>The remote_login_passwordfile setting specifies whether or not Oracle checks for a password file during login and how many databases can use the password file.</Control_Description>
Prompt			<Control_Risk>As the use of this sort of password login file could permit unsecured, privileged connections to the database, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the REMOTE_LOGIN_PASSWORDFILE should be set to 'None' ALTER SYSTEM SET REMOTE_LOGIN_PASSWORDFILE = 'NONE' SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LOGIN_PASSWORDFILE';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LOGIN_PASSWORDFILE';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET REMOTE_LOGIN_PASSWORDFILE = 'NONE' SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>NONE</Recommended_Value>
Prompt         <Comments>Control becomes NON-COMPLIANT when REMOTE_LOGIN_PASSWORDFILE has not been set to "NONE" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LOGIN_PASSWORDFILE';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to NONE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>100</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:1</CIS_Number>
Prompt			<Control_Name>TRACE_FILES_PUBLIC</Control_Name>
Prompt			<Control_Description>The _trace_files_public setting determines whether or not the systems trace file is world readable.</Control_Description>
Prompt			<Control_Risk>As permitting the read permission to other anyone can read the instances trace files file which could contain sensitive information about instance operations, this value should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the _TRACE_FILES_PUBLIC should be set to 'False' ALTER SYSTEM SET "_trace_files_public" = FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT VALUE FROM V$PARAMETER WHERE NAME='_trace_files_public';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT VALUE FROM V$PARAMETER WHERE NAME='_trace_files_public';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET "_trace_files_public" = FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt            <Comments>Control becomes NON-COMPLIANT when TRACE_FILES_PUBLIC has not been set to "FALSE" </Comments>
Prompt <Actual_Value>
SELECT VALUE FROM V$PARAMETER WHERE NAME='_trace_files_public';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>A VALUE equal to FALSE or lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>101</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:4:2</CIS_Number>
Prompt			<Control_Name>AUDIT_SYS_OPERATIONS</Control_Name>
Prompt			<Control_Description>The AUDIT_SYS_OPERATIONS setting provides for the auditing of all user activities conducted under the SYSOPER and SYSDBA accounts.</Control_Description>
Prompt			<Control_Risk>If the parameter AUDIT_SYS_OPERATIONS is FALSE all statements except of Startup/Shutdown and Logon by SYSDBA/SYSOPER users are not audited.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the AUDIT_SYS_OPERATIONS should be set to 'True' ALTER SYSTEM SET AUDIT_SYS_OPERATIONS = TRUE SCOPE=SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME) = 'AUDIT_SYS_OPERATIONS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement. SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME) = 'AUDIT_SYS_OPERATIONS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET AUDIT_SYS_OPERATIONS = TRUE SCOPE=SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>TRUE</Recommended_Value>
Prompt          <Comments>Control becomes NON-COMPLIANT when AUDIT_SYS_OPERATIONS has not been set to "TRUE" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME) = 'AUDIT_SYS_OPERATIONS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to TRUE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>102</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:4:3</CIS_Number>
Prompt			<Control_Name>AUDIT_TRAIL is set to 'OS', 'DB', 'XML', 'DB,EXTENDED', or 'XML,EXTENDED'</Control_Name>
Prompt			<Control_Description>The audit_trail setting determines whether or not Oracles basic audit features are enabled. These can be set to "Operating System"(OS), "DB,", "DB,EXTENDED", "XML" or "XML,EXTENDED".</Control_Description>
Prompt			<Control_Risk>As enabling the basic auditing features for the Oracle instance permits the collection of data to troubleshoot problems, as well as providing value forensic logs in the case of a system breach, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the Audit_Trail should be set properly;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='AUDIT_TRAIL';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='AUDIT_TRAIL';
Prompt 2. To remediate this setting execute one of the following SQL statements.
Prompt # ALTER SYSTEM SET AUDIT_TRAIL = DB SCOPE = SPFILE;
Prompt # ALTER SYSTEM SET AUDIT_TRAIL = DB, EXTENDED SCOPE = SPFILE;
Prompt # ALTER SYSTEM SET AUDIT_TRAIL = OS SCOPE = SPFILE;
Prompt # ALTER SYSTEM SET AUDIT_TRAIL = XML SCOPE = SPFILE;
Prompt # ALTER SYSTEM SET AUDIT_TRAIL = XML, EXTENDED SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>CONTAINS1</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when Audit_Trail has not been set to "DB;OS;XML;EXTENDED" </Comments>
Prompt			<Recommended_Value>DB;OS;XML;EXTENDED</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='AUDIT_TRAIL';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to OS or DB,EXTENDED or XML,EXTENDED.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>103</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:4</CIS_Number>
Prompt			<Control_Name>DICTIONARY ACCESSIBILITY </Control_Name>
Prompt			<Control_Description>The O7_dictionary_accessibility setting is a database initializations parameter that allows/disallows with the EXECUTE ANY PROCEDURE and SELECT ANY DICTIONARY access to objects in the SYS schema; this functionality was created for the ease of migration from Oracle 7 databases to later versions.</Control_Description>
Prompt			<Control_Risk>As leaving the SYS schema so open to connection could permit unauthorized access to critical data structures, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the O7_DICTIONARY_ACCESSIBILITY  should be set to 'False' ALTER SYSTEM SET O7_DICTIONARY_ACCESSIBILITY=FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='O7_DICTIONARY_ACCESSIBILITY';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='O7_DICTIONARY_ACCESSIBILITY';
Prompt 2. To remediate this setting execute the following SQL statement:
Prompt # ALTER SYSTEM SET O7_DICTIONARY_ACCESSIBILITY=FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DICTIONARY ACCESSIBILITY has not been set for "FALSE" </Comments>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='O7_DICTIONARY_ACCESSIBILITY';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>104</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:5</CIS_Number>
Prompt			<Control_Name>GLOBAL_NAMES</Control_Name>
Prompt			<Control_Description>The global_names setting requires that the name of a database link matches that of the remote database it will connect to.</Control_Description>
Prompt			<Control_Risk>As not requiring database connections to match the domain that is being called remotely could allow unauthorized domain sources to potentially connect via brute-force tactics, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the GLOBAL_NAMES should be set to 'True' ALTER SYSTEM SET GLOBAL_NAMES = TRUE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='GLOBAL_NAMES';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='GLOBAL_NAMES';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET GLOBAL_NAMES = TRUE SCOPE = SPFILE</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when GLOBAL_NAMES has not been set for "TRUE" </Comments>
Prompt			<Recommended_Value>TRUE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='GLOBAL_NAMES';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to TRUE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>105</S_No>
Prompt			<Category>Oracle-12C:4:6</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:6</CIS_Number>
Prompt			<Control_Name>LOCAL_LISTENER is Set Appropriately</Control_Name>
Prompt			<Control_Description>The local_listener setting specifies a network name that resolves to an address of the Oracle TNS listener.</Control_Description>
Prompt			<Control_Risk>The TNS poisoning attack allows to redirect TNS network traffic to another system by registering a listener to the TNS listener. This attack can be performed by unauthorized users with network access. By specifying the IPC protocol it is no longer possible to register listeners via TCP/IP.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the LOCAL_LISTENER='[description]' SCOPE should be set appropriately</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='LOCAL_LISTENER';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='LOCAL_LISTENER';
Prompt 2. To remediate this setting execute the following SQL statement:
Prompt ALTER SYSTEM SET LOCAL_LISTENER='[description]' SCOPE = BOTH;
Prompt 3. Replace [description] with the appropriate description from your listener.ora file, where that description sets the PROTOCOL parameter to IPC. For example:
Prompt ALTER SYSTEM SET LOCAL_LISTENER='(DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=REGISTER)))' SCOPE=BOTH;</Control_Recommendation>
Prompt			<Operation>MANUAL</Operation>
Prompt          <Comments>NA</Comments>
Prompt			<Recommended_Value>(DESCRIPTION=(ADDRESS= (PROTOCOL=IPC)(KEY=REGISTER)))</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='LOCAL_LISTENER';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to (DESCRIPTION=(ADDRESS= (PROTOCOL=IPC)(KEY=REGISTER))).</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>106</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:7</CIS_Number>
Prompt			<Control_Name>OS_ROLES</Control_Name>
Prompt			<Control_Description>The os_roles setting permits externally created groups to be applied to database management.</Control_Description>
Prompt			<Control_Risk>As allowing the OS use external groups for database management could cause privilege overlaps and generally weaken security, this value should be set according to the needs of the organization</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the OS_ROLES should be set to 'False' ALTER SYSTEM SET OS_ROLES = FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='OS_ROLES';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='OS_ROLES';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET OS_ROLES = FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when OS_ROLES has not been set to "FALSE" </Comments>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='OS_ROLES';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>107</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:8</CIS_Number>
Prompt			<Control_Name>REMOTE_LISTENER</Control_Name>
Prompt			<Control_Description>The remote_listener setting determines whether or not a valid listener can be established on a system separate from the database instance.</Control_Description>
Prompt			<Control_Risk>As permitting a remote listener for connections to the database instance can allow for the potential spoofing of connections and that could compromise data confidentiality and integrity, this value should be disabled/restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the OS_ROLES should be set to 'Empty' ALTER SYSTEM SET REMOTE_LISTENER = '' SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LISTENER';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LISTENER';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET REMOTE_LISTENER = '' SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when OS_ROLES has not been set to "Empty" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_LISTENER';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is empty.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>108</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:4:10</CIS_Number>
Prompt			<Control_Name>REMOTE_OS_AUTHENT</Control_Name>
Prompt			<Control_Description>The remote_os_authent setting determines whether or not OS 'roles' with the attendant privileges are allowed for remote client connections.</Control_Description>
Prompt			<Control_Risk>As permitting OS roles for database connections to can allow the spoofing of connections and permit granting the privileges of an OS role to unauthorized users to make connections, this value should be restricted according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the REMOTE_OS_AUTHENT should be set to 'False' ALTER SYSTEM SET REMOTE_OS_AUTHENT = FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_AUTHENT';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_AUTHENT';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET REMOTE_OS_AUTHENT = FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when REMOTE_OS_AUTHENT has not been set to "FALSE" </Comments>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_AUTHENT';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>109</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:4:11</CIS_Number>
Prompt			<Control_Name>REMOTE_OS_ROLES</Control_Name>
Prompt			<Control_Description>The remote_os_roles setting permits remote users OS roles to be applied to database management.</Control_Description>
Prompt			<Control_Risk>As allowing remote clients OS roles to have permissions for database management could cause privilege overlaps and generally weaken security, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure he REMOTE_OS_ROLES should be set to 'False' ALTER SYSTEM SET REMOTE_OS_ROLES = FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_ROLES';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_ROLES';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET REMOTE_OS_ROLES = FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt           <Comments>Control becomes NON-COMPLIANT when REMOTE_OS_ROLES has not been set to "FALSE" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='REMOTE_OS_ROLES';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>110</S_No>
Prompt			<Category>Database settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:12</CIS_Number>
Prompt			<Control_Name>RESOURCE_LIMIT</Control_Name>
Prompt			<Control_Description>RESOURCE_LIMIT determines whether resource limits are enforced in database profiles</Control_Description>
Prompt			<Control_Risk>If resource_limit is set to FALSE, none of the system resource limits that are set in any database profiles are enforced. If resource_limit is set to TRUE, then the limits set in database profiles are enforced.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the RESOURCE_LIMIT should be set to 'True':  ALTER SYSTEM SET RESOURCE_LIMIT = TRUE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='RESOURCE_LIMIT';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='RESOURCE_LIMIT';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET RESOURCE_LIMIT = TRUE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>TRUE</Recommended_Value>
Prompt        <Comments>Control becomes NON-COMPLIANT when RESOURCE_LIMIT has not been set to "TRUE" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='RESOURCE_LIMIT';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to TRUE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>111</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:13</CIS_Number>
Prompt			<Control_Name>SEC_CASE_SENSITIVE_LOGON</Control_Name>
Prompt			<Control_Description>The SEC_CASE_SENSITIVE_LOGON information determines whether or not case-sensitivity is required for passwords during login. Due to the security bug CVE-2012-3137 it is recommended to set this parameter to TRUE if the October 2012 CPU/PSU or later was applied. If the patch was not applied it is recommended to set this parameter to FALSE to avoid that the vulnerability could be abused.</Control_Description>
Prompt			<Control_Risk>Oracle 12c databases without CPU October 2012 patch or later are vulnerable to CVE- 2012-3137 if case-sensitive SHA-1 password hashes are used. To avoid this kind of attack the old DES-hashes have to be used.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SEC_CASE_SENSITIVE_LOGON should be set to 'True' : ALTER SYSTEM SET SEC_CASE_SENSITIVE_LOGON = TRUE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_CASE_SENSITIVE_LOGON';  Note: If SEC_CASE_SENSITIVE_LOGON is FALSE, all user with SHA-1 hashes only ("select name,password,spare4 from sys.user$ where password is null and spare4 is not null") are no longer able to connect to the database. In this case the password for all users without DES hash have to set again.</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_CASE_SENSITIVE_LOGON';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET SEC_CASE_SENSITIVE_LOGON = TRUE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt			<Recommended_Value>TRUE</Recommended_Value>
Prompt         <Comments>Control becomes NON-COMPLIANT when SEC_CASE_SENSITIVE_LOGON has not been set to "TRUE" </Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_CASE_SENSITIVE_LOGON';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to TRUE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>112</S_No>
Prompt			<Category>Prompt</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:14</CIS_Number>
Prompt			<Control_Name>SEC_MAX_FAILED_LOGIN_ATTEMPTS</Control_Name>
Prompt			<Control_Description>The SEC_MAX_FAILED_LOGIN_ATTEMPTS parameter determines how many failed login attempts are allowed before Oracle closes the login connection.</Control_Description>
Prompt			<Control_Risk>As allowing an unlimited number of login attempts for a user connection can facilitate both brute-force login attacks and the occurrence of Denial-of-Service , this value (10) should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the MAX_FAILED_LOGIN_ATTEMPTS should be set to '3' ALTER SYSTEM SET SEC_MAX_FAILED_LOGIN_ATTEMPTS = 3 SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_MAX_FAILED_LOGIN_ATTEMPTS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_MAX_FAILED_LOGIN_ATTEMPTS';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET SEC_MAX_FAILED_LOGIN_ATTEMPTS = 3 SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>LESSER</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when SEC_MAX_FAILED_LOGIN_ATTEMPTS has not been set to "3" </Comments>
Prompt			<Recommended_Value>3</Recommended_Value>

Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_MAX_FAILED_LOGIN_ATTEMPTS';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to 3.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>113</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:15</CIS_Number>
Prompt			<Control_Name>SEC_PROTOCOL_ERROR_FURTHER_ACTION</Control_Name>
Prompt			<Control_Description>The SEC_PROTOCOL_ERROR_FURTHER_ACTION setting determines the Oracle's server's response to bad/malformed packets received from the client.</Control_Description>
Prompt			<Control_Risk>As bad packets received from the client can potentially indicate packet-based attacks on the system, such as "TCP SYN Flood" or "Smurf" attacks, which could result in a Denial-of- Service condition, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SEC_PROTOCOL_ERROR_FURTHER_ACTION should be set to 'DELAY,3' or 'DROP,3'</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_FURTHER_ACTION';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_FURTHER_ACTION';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET SEC_PROTOCOL_ERROR_FURTHER_ACTION = 'DELAY,3' SCOPE = SPFILE; 
Prompt # ALTER SYSTEM SET SEC_PROTOCOL_ERROR_FURTHER_ACTION = 'DROP,3' SCOPE = SPFILE;;</Control_Recommendation>
Prompt			<Operation>CONTAINS1</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when SEC_PROTOCOL_ERROR_FURTHER_ACTION has not been set to "DELAY,3 or DROP,3" </Comments>
Prompt			<Recommended_Value>DELAY,3;DROP,3</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_FURTHER_ACTION';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to DELAY,3 or DROP,3.</Audit_Reference>
Prompt		</Control>
Prompt      <Control>
Prompt			<S_No>114</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:16</CIS_Number>
Prompt			<Control_Name>SEC_PROTOCOL_ERROR_TRACE_ACTION</Control_Name>
Prompt			<Control_Description>The SEC_PROTOCOL_ERROR_TRACE_ACTION setting determines the Oracle's server's logging response level to bad/malformed packets received from the client, by generating ALERT, LOG, or TRACE levels of detail in the log files.</Control_Description>
Prompt			<Control_Risk>As bad packets received from the client can potentially indicate packet-based attacks on the system, such as "TCP SYN Flood" or "Smurf" attacks, which could result in a Denial-of- Service condition, this diagnostic/logging value for ALERT, LOG, or TRACE conditions should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SEC_PROTOCOL_ERROR_TRACE_ACTION should be set to 'None' ALTER SYSTEM SET SEC_PROTOCOL_ERROR_TRACE_ACTION=LOG SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_TRACE_ACTION';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_TRACE_ACTION';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET SEC_PROTOCOL_ERROR_TRACE_ACTION=LOG SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>CONTAINS1</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SEC_PROTOCOL_ERROR_TRACE_ACTION has not been set to "TRACE or LOG"</Comments>
Prompt			<Recommended_Value>TRACE;LOG</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_PROTOCOL_ERROR_TRACE_ACTION';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to LOG.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>115</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:17</CIS_Number>
Prompt			<Control_Name>SEC_RETURN_SERVER_RELEASE_BANNER</Control_Name>
Prompt			<Control_Description>The information about patch/update release number provides information about the exact patch/update release that is currently running on the database.</Control_Description>
Prompt			<Control_Risk>As allowing the database to return information about the patch/update release number could facilitate unauthorized users attempts to gain access based upon known patch weaknesses, this value should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SEC_RETURN_SERVER_RELEASE_BANNER should be set to 'False' ALTER SYSTEM SET SEC_RETURN_SERVER_RELEASE_BANNER = FALSE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_RETURN_SERVER_RELEASE_BANNER';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_RETURN_SERVER_RELEASE_BANNER';
Prompt 2. To remediate this setting execute the following SQL statement: 
Prompt # ALTER SYSTEM SET SEC_RETURN_SERVER_RELEASE_BANNER = FALSE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SEC_RETURN_SERVER_RELEASE_BANNER has not been set to "FALSE"</Comments>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SEC_RETURN_SERVER_RELEASE_BANNER';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>116</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:18</CIS_Number>
Prompt			<Control_Name>SECURE_CONTROL_[listener_name]is set in 'listener.ora'</Control_Name>
Prompt			<Control_Description>The SECURE_CONTROL_listener_name setting determines the type of control connection the Oracle server requires for remote configuration of the listener.</Control_Description>
Prompt			<Control_Risk>As listener configuration changes via unencrypted remote connections can result in unauthorized users sniffing the control configuration information from the network, these control values should be set according to the needs of the organization.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SECURE_CONTROL_listener_name for each defined listener in the listener.ora file, according to the needs of the organization.</Agreed_Value>
Prompt			<Control_Parameter_1></Control_Parameter_1>
Prompt			<Control_Recommendation>1. To audit this recommendation, follow these steps: 
Prompt A. Open the $ORACLE_HOME/network/admin/listener.ora file (or %ORACLE_HOME%\network\admin\listener.ora on Windows)
Prompt B. Ensure that each defined listener as an associated SECURE_CONTROL_listener_name directive.
Prompt2. Set the SECURE_CONTROL_listener_name for each defined listener in the listener.ora file, according to the needs of the organizati</Control_Recommendation>
Prompt			<Operation>MANUAL</Operation>
Prompt          <Comments>NA</Comments>
Prompt <Actual_Value>

Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to FALSE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>117</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>2.2.17</CIS_Number>
Prompt			<Control_Name>SQL92_SECURITY</Control_Name>
Prompt			<Control_Description>The sql92_security parameter setting FALSE allows to grant only UPDATE or DELETE privileges without the need to grant SELECT privileges.</Control_Description>
Prompt			<Control_Risk>The default value TRUE of the parameter sql92_security is secure out-of-the-box. Several security guides recommend the unsecure setting FALSE. This unsecure setting FALSE allows users to UPDATE/DELETE privileges to select data directly instead of guessing it.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the SQL92_SECURITY should be set to 'True' ALTER SYSTEM SET SQL92_SECURITY = TRUE SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SQL92_SECURITY';</Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL statement.
Prompt SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SQL92_SECURITY';
Prompt 2. To remediate this setting execute the following SQL statement:
Prompt # ALTER SYSTEM SET SQL92_SECURITY = TRUE SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when SQL92_SECURITY has not been set to "FALSE"</Comments>
Prompt			<Recommended_Value>FALSE</Recommended_Value>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='SQL92_SECURITY';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is set to SCOPE.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>118</S_No>
Prompt			<Category>Protecting Resources</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:4:20</CIS_Number>
Prompt			<Control_Name>UTIL_FILE_DIR</Control_Name>
Prompt			<Control_Description>The utl_file_dir setting allows packages like utl_file to access (read/write/modify/delete) files specified in utl_file_dir. (This is deprecated but usable in 12c.)</Control_Description>
Prompt			<Control_Risk>As using the utl_file_dir to create directories allows the manipulation of files in these directories.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure the UTL_FILE_DIR should be set to 'Empty':  ALTER SYSTEM SET UTL_FILE_DIR = '' SCOPE = SPFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='UTIL_FILE_DIR';</Control_Parameter_1>
Prompt			<Control_Recommendation>Ensure the UTL_FILE_DIR should be set to 'Empty': ALTER SYSTEM SET UTL_FILE_DIR = '' SCOPE = SPFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when UTIL_FILE_DIR has not been set to "Empty"</Comments>
Prompt <Actual_Value>
SELECT UPPER(VALUE) FROM V$PARAMETER WHERE UPPER(NAME)='UTIL_FILE_DIR';
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>Ensure VALUE is empty.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>119</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:1</CIS_Number>
Prompt			<Control_Name>Enable ALTER DATABASE LINK Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER DATABASE or ALTER PUBLIC DATABASE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER DATABASE LINK Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALTER DATABASE LINK;</Agreed_Value>
Prompt			<Control_Parameter_1>AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES  AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED  WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES  AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY'  AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD  ACTIONS ALTER DATABASE LINK;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when  ALTER DATABASE LINK Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES  AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED  WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>120</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:2</CIS_Number>
Prompt			<Control_Name>Enable ALTER PROFILE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER PROFILE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such  statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER PROFILE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALTER PROFILE</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS 
Prompt ALTER PROFILE; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALTER PROFILE Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>121</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:3</CIS_Number>
Prompt			<Control_Name>Enable ALTER ROLE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER ROLE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER ROLE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS ALTER ROLE</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS ALTER ROLE;  </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALTER ROLE Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>

Prompt		<Control>
Prompt			<S_No>122</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:4</CIS_Number>
Prompt			<Control_Name>Enable ALTER SYNONYM Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER SYNONYM or ALTER PUBLIC SYNONYM statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.  </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE SYNONYM Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS ALTER SYNONYM</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS ALTER SYNONYM; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when ALTER SYNONYM Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>123</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:5</CIS_Number>
Prompt			<Control_Name>Enable ALTER SYSTEM Privilege</Control_Name>
Prompt			<Control_Description>This unified audit enables logging of activities that involve exercise of this privilege, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER SYSTEM Privilege should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALTER SYSTEM;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYSTEM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYSTEM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS  ALTER SYSTEM;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when ALTER SYSTEM Privilege Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER SYSTEM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>124</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:6</CIS_Number>
Prompt			<Control_Name>Enable ALTER TRIGGER Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER TRIGGER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Unauthorized alteration of triggers may impact critical business functions or compromise integrity/security of the database. Logging and monitoring of all attempts to alter triggers, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER TRIGGER should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALTER TRIGGER</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS  ALTER TRIGGER;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when ALTER TRIGGER Privilege Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>125</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:7</CIS_Number>
Prompt			<Control_Name>Enable ALTER USER Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all ALTER USER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure ALTER USER Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALTER USER; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS ALTER USER; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when ALTER USER Privilege Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALTER USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>126</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:8</CIS_Number>
Prompt			<Control_Name>Enable CREATE DATABASE LINK Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE DATABASE or CREATE PUBLIC DATABASE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE DATABASE LINK Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE DATABASE LINK;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS CREATE DATABASE LINK; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when CREATE DATABASE LINK Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>127</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:9</CIS_Number>
Prompt			<Control_Name>Enable CREATE PROFILE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE PROFILE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE PROFILE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE PROFILE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  

Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS CREATE PROFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when CREATE PROFILE Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>128</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:10</CIS_Number>
Prompt			<Control_Name>Enable CREATE ROLE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE ROLE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE ROLE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE ROLE;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS CREATE ROLE; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when CREATE ROLE Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>129</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:11</CIS_Number>
Prompt			<Control_Name>Enable CREATE SYNONYM Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE SYNONYM or CREATE PUBLIC SYNONYM statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE SYNONYM Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE SYNONYM;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS CREATE SYNONYM;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when CREATE SYNONYM Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>130</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:12</CIS_Number>
Prompt			<Control_Name>Enable CREATE TRIGGER Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE TRIGGER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE TRIGGER should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE TRIGGER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>11.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS  CREATE TRIGGER;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt            <Comments>Control becomes NON-COMPLIANT when CREATE TRIGGER Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>131</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:13</CIS_Number>
Prompt			<Control_Name>Enable CREATE USER Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all CREATE  USER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure CREATE USER Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS CREATE USER; </Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1. To verify this recommendation, execute the following SQL Statement. SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS CREATE USER; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when CREATE USER Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'CREATE USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>132</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:14</CIS_Number>
Prompt			<Control_Name>Enable DROP DATABASE LINK Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP DATABASE or DROP PUBLIC DATABASE, whether successful or unsuccessful, statements issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP DATABASE LINK Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS DROP DATABASE LINK;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS DROP DATABASE LINK;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DROP DATABASE LINK Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP DATABASE LINK' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>133</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:15</CIS_Number>
Prompt			<Control_Name>Enable DROP PROFILE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP PROFILE statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP PROFILE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS DROP PROFILE</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS DROP PROFILE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when DROP PROFILE  Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP PROFILE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>134</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:16</CIS_Number>
Prompt			<Control_Name>Enable DROP ROLE Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP ROLE statements, successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP ROLE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS DROP ROLE</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES  AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS DROP ROLE;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DROP ROLE  Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP ROLE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>135</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:17</CIS_Number>
Prompt			<Control_Name>Enable DROP SYNONYM Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP SYNONYM or DROP PUBLIC SYNONYM statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP SYNONYM Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS DROP SYNONYM</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS DROP SYNONYM;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when DROP SYNONYM  Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP SYNONYM' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>136</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:18</CIS_Number>
Prompt			<Control_Name>Enable DROP TRIGGER Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP TRIGGER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Unauthorized alteration of triggers may impact critical business functions or compromise integrity/security of the database. Logging and monitoring of all attempts to alter triggers, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP TRIGGER should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS DROP TRIGGER</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD  ACTIONS  DROP TRIGGER;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt        <Comments>Control becomes NON-COMPLIANT when DROP TRIGGER  Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP TRIGGER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';  
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>137</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:19</CIS_Number>
Prompt			<Control_Name>Enable DROP USER Audit</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all DROP USER statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to create user, whether successful or unsuccessful, may provide clues and forensic evidences about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure DROP USER Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS DROP USER;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS';   </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'DROP USER' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS DROP USER;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt        <Comments>Control becomes NON-COMPLIANT when DROP USER Audit has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUDIT_OPTION, SUCCESS, FAILURE FROM DBA_STMT_AUDIT_OPTS WHERE AUDIT_OPTION='DROP USER' AND USER_NAME IS NULL AND PROXY_NAME IS NULL AND SUCCESS = 'BY ACCESS' AND FAILURE = 'BY ACCESS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>138</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:20</CIS_Number>
Prompt			<Control_Name>Enable GRANT Action</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all GRANT statements, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>A malicious user may be able to change the security of the database, access/update confidential data or compromise integrity of the database. Logging and monitoring of all attempts to grant system privileges, object privileges or roles, whether successful or unsuccessful, may provide forensic evidence about potential suspicious/unauthorized activities as well as privilege escalation activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure GRANT Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS GRANT;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'GRANT' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'</Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'GRANT' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS GRANT; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when GRANT Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE 
FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED 
WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME 
AND AUD.AUDIT_OPTION = 'GRANT' 
AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' 
AND ENABLED.SUCCESS = 'YES' 
AND ENABLED.FAILURE = 'YES' 
AND ENABLED.ENABLED_OPT = 'BY' 
AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>139</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:21</CIS_Number>
Prompt			<Control_Name>Enable LOGON/LOGOFF Actions</Control_Name>
Prompt			<Control_Description>This unified audit action enables logging of all LOGON actions, whether successful or unsuccessful, issued by the users regardless of the privileges held by the users to log into the database. In addition, LOGOFF action audit captures logoff activities. This audit action also captures logon/logoff to the open database by SYSDBA and SYSOPE</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure LOGON/LOGOFF should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS LOGON, LOGOFF;</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT * FROM AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGON' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION')  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGOFF' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION');</Control_Parameter_1>	
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT * FROM AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGON' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION')  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGOFF' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION');
Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  
Prompt ADD ACTIONS  LOGON,  LOGOFF; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt         <Comments>Control becomes NON-COMPLIANT when LOGON/LOGOFF Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT * FROM AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGON' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION')  AND EXISTS ( SELECT 'x'  FROM AUDIT_UNIFIED_POLICIES  AUD WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'LOGOFF' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION');
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>140</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:22</CIS_Number>
Prompt			<Control_Name>Enable REVOKE Action</Control_Name>
Prompt			<Control_Description>REVOKE SQL statements are used to revoke privileges from Oracle database users and roles. This unified audit action enables logging of all REVOKE statements, successful or unsuccessful, issued by the users regardless of the privileges held by the users to issue such statements.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure REVOKE Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS REVOKE</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'REVOKE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';</Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'REVOKE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt 2. Execute the following SQL statement to remediate this setting. # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS REVOKE;  </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when REVOKE Action has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'REVOKE' AND AUD.AUDIT_OPTION_TYPE = 'STANDARD ACTION' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>141</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>Medium</Severity>
Prompt			<CIS_Number>Oracle-12C:5:23</CIS_Number>
Prompt			<Control_Name>Enable SELECT ANY DICTIONARY Privilege</Control_Name>
Prompt			<Control_Description>SELECT ANY DICTIONARY system privilege allows the user to view the definition of all schema objects in the database. It grants SELECT privileges on the data dictionary objects to the grantees, including SELECT on DBA_ views, V$ views, X$ views and underlying SYS tables such as TAB$, OBJ$, etc. This privilege also allows grantees to create stored objects such as procedures, packages or views on the underlying data dictionary objects.</Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure SELECT ANY DICTIONARY Action should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD PRIVILEGES SELECT ANY DICTIONARY</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'SELECT ANY DICTIONARY' AND AUD.AUDIT_OPTION_TYPE = 'SYSTEM PRIVILEGE' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'SELECT ANY DICTIONARY' AND AUD.AUDIT_OPTION_TYPE = 'SYSTEM PRIVILEGE' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';
Prompt 2. Execute the following SQL statement to remediate this setting. # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD PRIVILEGES SELECT ANY DICTIONARY;</Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt           <Comments>Control becomes NON-COMPLIANT when SELECT ANY DICTIONARY has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'SELECT ANY DICTIONARY' AND AUD.AUDIT_OPTION_TYPE = 'SYSTEM PRIVILEGE' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt		<Control>
Prompt			<S_No>142</S_No>
Prompt			<Category>Security Settings</Category>
Prompt			<Severity>High</Severity>
Prompt			<CIS_Number>Oracle-12C:5:24</CIS_Number>
Prompt			<Control_Name>Enable UNIFIED_AUDIT_TRAIL Access</Control_Name>
Prompt			<Control_Description>UNIFIED_AUDIT_TRAIL view holds audit trail records generated by the database. This audit action enables logging of all access attempts to the UNIFIED_AUDIT_TRAIL view, whether successful or unsuccessful, regardless of the privileges held by the users to issue such statements. </Control_Description>
Prompt			<Control_Risk>Logging and monitoring of all attempts to revoke system privileges, object privileges or roles, whether successful or unsuccessful, may provide clues and forensic evidence about potential suspicious/unauthorized activities.</Control_Risk>
Prompt			<Control_Type>SQL_POLICY</Control_Type>
Prompt          <Agreed_Value>Ensure UNIFIED_AUDIT_TRAIL Access should be enabled ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY ADD ACTIONS ALL on SYS.UNIFIED_AUDIT_TRAIL</Agreed_Value>
Prompt			<Control_Parameter_1>SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALL' AND AUD.AUDIT_OPTION_TYPE = 'OBJECT ACTION' AND AUD.OBJECT_SCHEMA = 'SYS' AND AUD.OBJECT_NAME = 'UNIFIED_AUDIT_TRAIL' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; </Control_Parameter_1>
Prompt			<Control_Recommendation>1.  To verify this recommendation, execute the following SQL statement. 
Prompt SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALL' AND AUD.AUDIT_OPTION_TYPE = 'OBJECT ACTION' AND AUD.OBJECT_SCHEMA = 'SYS' AND AUD.OBJECT_NAME = 'UNIFIED_AUDIT_TRAIL' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS';

Prompt 2. Execute the following SQL statement to remediate this setting. 
Prompt # ALTER AUDIT POLICY CIS_UNIFIED_AUDIT_POLICY  ADD ACTIONS  ALL on SYS.UNIFIED_AUDIT_TRAIL; </Control_Recommendation>
Prompt			<Operation>EQUALS</Operation>
Prompt          <Comments>Control becomes NON-COMPLIANT when UNIFIED_AUDIT_TRAIL Access has not been Enabled</Comments>
Prompt <Actual_Value>
SELECT AUD.POLICY_NAME, AUD.AUDIT_OPTION, AUD.AUDIT_OPTION_TYPE FROM AUDIT_UNIFIED_POLICIES AUD, AUDIT_UNIFIED_ENABLED_POLICIES ENABLED WHERE AUD.POLICY_NAME = ENABLED.POLICY_NAME AND AUD.AUDIT_OPTION = 'ALL' AND AUD.AUDIT_OPTION_TYPE = 'OBJECT ACTION' AND AUD.OBJECT_SCHEMA = 'SYS' AND AUD.OBJECT_NAME = 'UNIFIED_AUDIT_TRAIL' AND ENABLED.SUCCESS = 'YES' AND ENABLED.FAILURE = 'YES' AND ENABLED.ENABLED_OPT = 'BY' AND ENABLED.USER_NAME = 'ALL USERS'; 
Prompt </Actual_Value>
Prompt <Hostname>
SELECT UTL_INADDR.get_host_name FROM dual;
Prompt </Hostname>
Prompt			<Audit_Reference>lack of results implies compliance.</Audit_Reference>
Prompt		</Control>
Prompt	</Oracle12c>
set heading on
spool off
