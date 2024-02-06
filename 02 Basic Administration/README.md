# Basic Administration

## Create Database
### By cli
```
CREATE DATABASE testdb
   USER SYS IDENTIFIED BY sys_password
   USER SYSTEM IDENTIFIED BY system_password
   LOGFILE GROUP 1 ('/u01/logs/my/redo01a.log','/u02/logs/my/redo01b.log') SIZE 100M,
           GROUP 2 ('/u01/logs/my/redo02a.log','/u02/logs/my/redo02b.log') SIZE 100M,
           GROUP 3 ('/u01/logs/my/redo03a.log','/u02/logs/my/redo03b.log') SIZE 100M
   MAXLOGHISTORY 1
   MAXLOGFILES 16
   MAXLOGMEMBERS 3
   MAXDATAFILES 1024
   CHARACTER SET AL32UTF8
   NATIONAL CHARACTER SET AL16UTF16
   EXTENT MANAGEMENT LOCAL
   DATAFILE '/u01/app/oracle/oradata/mynewdb/system01.dbf'
     SIZE 700M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   SYSAUX DATAFILE '/u01/app/oracle/oradata/mynewdb/sysaux01.dbf'
     SIZE 550M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   DEFAULT TABLESPACE users
      DATAFILE '/u01/app/oracle/oradata/mynewdb/users01.dbf'
      SIZE 500M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED
   DEFAULT TEMPORARY TABLESPACE tempts1
      TEMPFILE '/u01/app/oracle/oradata/mynewdb/temp01.dbf'
      SIZE 20M REUSE AUTOEXTEND ON NEXT 640K MAXSIZE UNLIMITED
   UNDO TABLESPACE undotbs1
      DATAFILE '/u01/app/oracle/oradata/mynewdb/undotbs01.dbf'
      SIZE 200M REUSE AUTOEXTEND ON NEXT 5120K MAXSIZE UNLIMITED
   USER_DATA TABLESPACE usertbs
      DATAFILE '/u01/app/oracle/oradata/mynewdb/usertbs01.dbf'
      SIZE 200M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED;
```

### Using DBCA
```
dbca
```

![step 1](/02%20Basic%20Administration/img/step%201.png)
![step 1](/02%20Basic%20Administration/img/step%202.png)
![step 1](/02%20Basic%20Administration/img/step%203.png)
![step 1](/02%20Basic%20Administration/img/step%204.png)
![step 1](/02%20Basic%20Administration/img/step%205.png)
![step 1](/02%20Basic%20Administration/img/step%206.png)
![step 1](/02%20Basic%20Administration/img/step%207.png)
![step 1](/02%20Basic%20Administration/img/step%208.png)
![step 1](/02%20Basic%20Administration/img/step%209.png)
![step 1](/02%20Basic%20Administration/img/step%2010.png)
![step 1](/02%20Basic%20Administration/img/step%2011.png)
![step 1](/02%20Basic%20Administration/img/step%2012.png)
![step 1](/02%20Basic%20Administration/img/step%2013.png)
![step 1](/02%20Basic%20Administration/img/step%2014.png)
![step 1](/02%20Basic%20Administration/img/step%2015.png)
![step 1](/02%20Basic%20Administration/img/step%2016.png)