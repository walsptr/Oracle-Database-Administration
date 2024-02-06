# Basic Administration

## Create Database
### By cli
```
CREATE DATABASE testdb
   USER SYS IDENTIFIED BY password
   USER SYSTEM IDENTIFIED BY password
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
Nantinya akan muncul windows seperti gambar dibawah. Pada bagian ini pilih yang Create a database.
![step 1](/02%20Basic%20Administration/img/step%201.png)

Pada tab Creation Mode pilih yang Advanced configuration.
![step 2](/02%20Basic%20Administration/img/step%202.png)

Pada bagian Deployment Type untuk Database Type biarkan default ke Oracle Single Instance database. Dibagian Template name kalian bisa tentukan sendiri, disini saya memilih yang Custom Database.
![step 3](/02%20Basic%20Administration/img/step%203.png)

Dibagian Database Identification, isikan Nama Database dan juga SID nya. Ini digunakan sebagai identifier untuk koneksi Database nantinya. Uncheck pada bagian Create as Container database. Disini kita tidak akan membuat container database dulu.
![step 4](/02%20Basic%20Administration/img/step%204.png)

Pada bagian Storage Option, pilih option Use following for the database storage attributes. Jangan lupa untuk centang bagian User Oracle-Managed File (OMF).

![step 5](/02%20Basic%20Administration/img/step%205.png)

Pada bagian Fast Recovery Option, centang di Specifiy Fast Recovery Area. Untuk bagian Fast Recovery Area size bisa disesuaikan.
![step 6](/02%20Basic%20Administration/img/step%206.png)

Pada bagian Network Configuration, disini kita akan menggunakan Listener yang telah kita buat sebelumnya. Cukup dicentang pada bagian Listenernya. Selain itu, disini kita juga dapat membuat listener juga.
![step 7](/02%20Basic%20Administration/img/step%207.png)

Pada bagian Database Options cukup pilih yang Oracle lVM.
![step 8](/02%20Basic%20Administration/img/step%208.png)

Pada bagian Configuration Options, di tab memory pilih yang Use Automatic Shared Memory Management.
![step 9](/02%20Basic%20Administration/img/step%209.png)

Pergi ke menut tab Sizing dan ubah processes menjadi 500. Bisa juga disesuaikan sesuai kebutuhan untuk berapa banyak processes yang di inginkan.
![step 10](/02%20Basic%20Administration/img/step%2010.png)

Pada bagian Management Options, centang pada Configure Enterprise Manager (EM) database express. Biarkan port nya default.
![step 11](/02%20Basic%20Administration/img/step%2011.png)

Pada bagian User Credential bisa disesuaikan. Jika ingin user SYS dan SYSTEM memiliki password yang berbeda pilih Use different administrative passwords. Sedangkan, jika ingin memiliki password yang sama bisa pilih Use the same administrative password for all accounts.
![step 12](/02%20Basic%20Administration/img/step%2012.png)

Pada bagian Creation Option kita pilih Create database, karena kita ingin membuat database nya langsung.
![step 13](/02%20Basic%20Administration/img/step%2013.png)

Pada bagian Summary kita lihat lagi konfigurasi kita, jika dirasa sudah benar langsung klik Finish.
![step 14](/02%20Basic%20Administration/img/step%2014.png)

Tunggu proses createnya selesai.
![step 15](/02%20Basic%20Administration/img/step%2015.png)

Jika sudah selesai bisa langsung klik Close
![step 16](/02%20Basic%20Administration/img/step%2016.png)