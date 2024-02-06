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
   DATAFILE '/opt/oracle/oradata/mynewdb/system01.dbf'
     SIZE 700M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   SYSAUX DATAFILE '/opt/oracle/oradata/mynewdb/sysaux01.dbf'
     SIZE 550M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   DEFAULT TABLESPACE users
      DATAFILE '/opt/oracle/oradata/mynewdb/users01.dbf'
      SIZE 500M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED
   DEFAULT TEMPORARY TABLESPACE tempts1
      TEMPFILE '/opt/oracle/oradata/mynewdb/temp01.dbf'
      SIZE 20M REUSE AUTOEXTEND ON NEXT 640K MAXSIZE UNLIMITED
   UNDO TABLESPACE undotbs1
      DATAFILE '/opt/oracle/oradata/mynewdb/undotbs01.dbf'
      SIZE 200M REUSE AUTOEXTEND ON NEXT 5120K MAXSIZE UNLIMITED
   USER_DATA TABLESPACE usertbs
      DATAFILE '/opt/oracle/oradata/mynewdb/usertbs01.dbf'
      SIZE 200M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED;
```

### Using DBCA
```
dbca
```
Nantinya akan muncul windows seperti gambar dibawah. Pada bagian ini pilih yang Create a database.
<br>
![step 1](/02%20Basic%20Administration/img/step%201.png)

Pada tab Creation Mode pilih yang Advanced configuration.
<br>
![step 2](/02%20Basic%20Administration/img/step%202.png)

Pada bagian Deployment Type untuk Database Type biarkan default ke Oracle Single Instance database. Dibagian Template name kalian bisa tentukan sendiri, disini saya memilih yang Custom Database.
<br>
![step 3](/02%20Basic%20Administration/img/step%203.png)

Dibagian Database Identification, isikan Nama Database dan juga SID nya. Ini digunakan sebagai identifier untuk koneksi Database nantinya. Uncheck pada bagian Create as Container database. Disini kita tidak akan membuat container database dulu.
<br>
![step 4](/02%20Basic%20Administration/img/step%204.png)

Pada bagian Storage Option, pilih option Use following for the database storage attributes. Jangan lupa untuk centang bagian User Oracle-Managed File (OMF).
<br>
![step 5](/02%20Basic%20Administration/img/step%205.png)

Pada bagian Fast Recovery Option, centang di Specifiy Fast Recovery Area. Untuk bagian Fast Recovery Area size bisa disesuaikan.
<br>
![step 6](/02%20Basic%20Administration/img/step%206.png)

Pada bagian Network Configuration, disini kita akan menggunakan Listener yang telah kita buat sebelumnya. Cukup dicentang pada bagian Listenernya. Selain itu, disini kita juga dapat membuat listener juga.
<br>
![step 7](/02%20Basic%20Administration/img/step%207.png)

Pada bagian Database Options cukup pilih yang Oracle lVM.
<br>
![step 8](/02%20Basic%20Administration/img/step%208.png)

Pada bagian Configuration Options, di tab memory pilih yang Use Automatic Shared Memory Management.
<br>
![step 9](/02%20Basic%20Administration/img/step%209.png)

Pergi ke menut tab Sizing dan ubah processes menjadi 500. Bisa juga disesuaikan sesuai kebutuhan untuk berapa banyak processes yang di inginkan.
<br>
![step 10](/02%20Basic%20Administration/img/step%2010.png)

Pada bagian Management Options, centang pada Configure Enterprise Manager (EM) database express. Biarkan port nya default.
<br>
![step 11](/02%20Basic%20Administration/img/step%2011.png)

Pada bagian User Credential bisa disesuaikan. Jika ingin user SYS dan SYSTEM memiliki password yang berbeda pilih Use different administrative passwords. Sedangkan, jika ingin memiliki password yang sama bisa pilih Use the same administrative password for all accounts.
<br>
![step 12](/02%20Basic%20Administration/img/step%2012.png)

Pada bagian Creation Option kita pilih Create database, karena kita ingin membuat database nya langsung.
<br>
![step 13](/02%20Basic%20Administration/img/step%2013.png)

Pada bagian Summary kita lihat lagi konfigurasi kita, jika dirasa sudah benar langsung klik Finish.
<br>
![step 14](/02%20Basic%20Administration/img/step%2014.png)

Tunggu proses createnya selesai.
<br>
![step 15](/02%20Basic%20Administration/img/step%2015.png)

Jika sudah selesai bisa langsung klik Close
<br>
![step 16](/02%20Basic%20Administration/img/step%2016.png)

## Managing Instance
Start instance
```
> startup
> startup open
> startup nomount
> startup mount
```
Stop Instance
```
> shutdown normal
> shutdown transactional
> shutdown immediate
> shutdown abort
```

## Managing Database Initialization Parameters
### Create pfile from spfile
lihat parameter spfile
```
> show parameter spfile

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
spfile                               string      /opt/oracle/product/19c/dbhome
                                                 _1/dbs/spfile(SID).ora

```
Membuat pfile
```
> create pfile='/home/oracle/pfile_test.conf' from spfile;
```


Melihat isi pfile
```
> less /home/oracle/pfile_test.conf
```

shutdown instance
```
> shutdown immediate
```

Rename spfile
```
$ cd $ORACLE_HOME/dbs
$ mv spfile(SID).ora ori_spfile(SID).ora
```

Jika kita start harusnya akan mendapatkan error karena tidak adanya file init param
```
> startup
```
Pindahkan pfile yang telah dibuat ke directory init parameter
```
$ cp /home/oracle/pfile_test.conf $ORACLE_HOME/dbs/init(SID).ora
```

Jalankan kembali instance
```
> startup
```

Kita cek kembali init paramnya
```
> show parameter spfile
```

### Recreate SPfile from Pfile



### Managing Data DIictionary