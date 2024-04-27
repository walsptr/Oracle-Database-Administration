# Basic Administration

## Create Database
### By cli
```
CREATE DATABASE testdb
   USER SYS IDENTIFIED BY password
   USER SYSTEM IDENTIFIED BY password
   LOGFILE GROUP 1 ('/opt/oracle/oradata/testdb/redo01b.log') SIZE 10M,
   MAXLOGHISTORY 1
   MAXLOGFILES 16
   MAXLOGMEMBERS 3
   MAXDATAFILES 1024
   CHARACTER SET AL32UTF8
   NATIONAL CHARACTER SET AL16UTF16
   EXTENT MANAGEMENT LOCAL
   DATAFILE '/opt/oracle/oradata/testdb/system01.dbf'
     SIZE 10M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   SYSAUX DATAFILE '/opt/oracle/oradata/testdb/sysaux01.dbf'
     SIZE 10M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
   DEFAULT TABLESPACE users
      DATAFILE '/opt/oracle/oradata/testdb/users01.dbf'
      SIZE 10M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED
   DEFAULT TEMPORARY TABLESPACE tempts1
      TEMPFILE '/opt/oracle/oradata/testdb/temp01.dbf'
      SIZE 10M REUSE AUTOEXTEND ON NEXT 640K MAXSIZE UNLIMITED
   UNDO TABLESPACE undotbs1
      DATAFILE '/opt/oracle/oradata/testdb/undotbs01.dbf'
      SIZE 10M REUSE AUTOEXTEND ON NEXT 5120K MAXSIZE UNLIMITED
   USER_DATA TABLESPACE usertbs
      DATAFILE '/opt/oracle/oradata/testdb/usertbs01.dbf'
      SIZE 10M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED;
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

### Show database
```
//melihat current database
show con_name;

//
select name from v$database;
```

## Managing Tablespace
### UNDO Tablespace
create
```
//create dir
mkdir /opt/oracle/oradata/<db-name>/ts

//create undo tablespace
create undo tablespace undotbs2 datafile '/opt/oracle/oradata/<db-name>/ts/undotbs2.dbf' size 10m;
```

resize
```
alter database datafile '/opt/oracle/oradata/<db-name>/ts/undotbs2.dbf' resize 20m;
```

add tbs
```
alter tablespace undotbs2 add datafile '/opt/oracle/oradata/<db-name>/ts/undotbs3.dbf' size 10m;
```

melihat datafile dan size tablespace
```
select file_name,bytes from dba_data_files;
```

melihat dir undo tablespace yang aktif
```
show parameter undo_tablespace
```

change default undo tablespace to new undo tablespace
```
alter system set undo_tablespace=undotbs2;
```

melihat freespace pada undo tablespace
```
select a.name, sum(b.bytes) from v$datafile a, dba_free_space b 
where a.file#=b.file_id and b.TABLESPACE_NAME='UNDOTBS2' group by 
a.name;
```

drop undo tablespace
```
drop tablespace undotbs2;
```

### Temporary Tablespace

create temp tablespace
```
create temporary tablespace temp2 tempfile '/opt/oracle/oradata/<db-name>/ts/temp2.dbf' size 10m;
```

resize temp tablespace
```
alter database tempfile '/opt/oracle/oradata/<db-name>/ts/temp2.dbf' resize 20m;
```

add temp tablespace
```
alter database temp2 add tempfile '/opt/oracle/oradata/<db-name>/ts/temp23.dbf' size 10m;
```

melihat dir temp tablespace yang ada
```
select file_name,bytes from dba_temp_files;
```

change default temporary tablespace
```

```

melihat free space temp tablespace
```
select a.name, sum(b.BYTES_FREE) from v$tempfile a, 
V$TEMP_SPACE_HEADER b where a.file#=b.file_id and 
b.TABLESPACE_NAME='TEMP2' group by a.name;
```

### Permanent Tablespace
Create permanent tablespace
```
create tablespace pdata datafile '/opt/oracle/oradata/<db-name>/ts/data2.dbf' size 10m;
```

resize permanent tablespace
```
alter database datafile '/opt/oracle/oradata/<db-name>/ts/data2.dbf' resize 20m;
```

add permanent tablespace
```
alter tablespace pdata add datafile '/opt/oracle/oradata/<db-name>/ts/data3.dbf' size 10m;
```

melihat default permanent tablespace
```
select PROPERTY_VALUE from database_properties where 
PROPERTY_NAME='DEFAULT_PERMANENT_TABLESPACE';
```

change default permanent tablespace to new tablespace
```
alter database default tablespace pdata;
```

### Managing table
create table

```
create table tb_test(id int primary key, name varchar (255));
```

insert data to table
```
insert into tb_test values(generate_series(1,10),'data'||generate_series(1,10));
```

show table
```
select * from all_tables;
```



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

Recreate SPfile from Pfile
```
$ sqlplus / as sysdba
> create spfile='/opt/oracle/product/19c/dbhome_1/dbs/spfile(SID).ora' FROM PFILE='/opt/oracle/product/19c/dbhome_1/dbs/init(SID).ora';
```

Lihat semua parameter file yang ada
```
$ls $ORACLE_HOME/dbs/*ora
/opt/oracle/product/19c/dbhome_1/dbs/init(SID).ora            //pfile we create
/opt/oracle/product/19c/dbhome_1/dbs/init.ora                 //example pfile
/opt/oracle/product/19c/dbhome_1/dbs/ori_spfile(SID).ora      //original spfile
/opt/oracle/product/19c/dbhome_1/dbs/spfile(SID).ora          //new spfile from pfile
```

Selanjutnya kita matikan dan jalankan kembali instancenya
```
> shutdown immediate
Database closed.
Database dismounted.
ORACLE instance shut down.
> startup
ORACLE instance started.
```

Sekarang kita cek dengan show parameter
```
> show parameter spfile

NAME                                 TYPE        VALUE
------------------------------------ ----------- ------------------------------
spfile                               string      /opt/oracle/product/19c/dbhome
                                                       _1/dbs/spfile(SID).ora
```
## Managing Data Dictionary
### Dynamic Performance Views
```
> SELECT * FROM V$MEMORY_DYNAMIC_COMPONENTS ;
> SELECT * FROM V$SESSION;
> SELECT LOG_MODE,OPEN_MODE,DATABASE_ROLE FROM V$DATABASE;
```

### Data Dictionary Views
```
> SELECT USERNAME, ACCOUNT_STATUS FROM DBA_USERS;
> SELECT TABLE_NAME, TABLESPACE_NAME FROM USER_TABLE;
```


## Move and Rename Datafile


Terkadang kita perlu memindahkan datafile dari satu disk ke disk yang lainnya. Atau kadang kita perlu merename datafile karena ada kesalahkan ketik atau semacamnya. Baik memindahkan atau merename datafile memiliki cara yang sama dalam mengelolanya.

Dsini saya akan mencoba merename suatu datafile temporary tablespace yang telah kita buat

### Move/rename database dalam mode noarchivelog
shutdown database
```
shutdown immediate
```

pindahkan atau rename datafile
```
# mv /opt/oracle/oradata/<db-name>/ts/temp2.dbf /opt/oracle/oradata/<db-name>/ts/temp3.dbf
```

start mount database
```
startup mount
```

rename datafile pada level database
```
alter database rename file '/opt/oracle/oradata/<db-name>/ts/temp2.dbf' to '/opt/oracle/oradata/<db-name>/ts/temp3.dbf';
```

open database
```
alter database open
```

### Move/rename database dalam mode archivelog

disini kita tidak perlu shutdown database. cukup offline kan filenya
```
alter database datafile '/opt/oracle/oradata/<db-name>/ts/temp2.dbf' offline;
```

mv/rename datafile
```
# mv /opt/oracle/oradata/<db-name>/ts/temp2.dbf /opt/oracle/oradata/<db-name>/ts/temp3.dbf
```

rename datafile dilevel database
```
alter database rename file '/opt/oracle/oradata/<db-name>/ts/temp2.dbf' to '/opt/oracle/oradata/<db-name>/ts/temp3.dbf';
```

recover datafile
```
recover datafile '/opt/oracle/oradata/<db-name>/ts/temp3.dbf';
```

online kan datafile
```
alter database datafile '/opt/oracle/oradata/<db-name>/ts/temp3.dbf';
```


## Managing Log and Trace
default trace log directory
```
/opt/oracle/diag/rdbms/<db-name>/<db-name>/trace/
```

default alert log dire
```
/opt/oracle/diag/rdbms/<db-name>/<db-name>/alert/

atau 

show parameter background_dump_dest
```

network log
```
$ORACLE_HOME/network/log
```