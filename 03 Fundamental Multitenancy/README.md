# Fundamental

### Create PDB using PDB$SEED

Untuk membuat PDB menggunakan PDB$SEED kita perlu menemukan terlebih dahulu directory PDB$SEED-nya. Masuk ke SQLPLUS dan jalankan perintah dibawah
```
> SELECT name from V$CONTAINERS;

NAME
---------------
CDB$ROOT
PDB$SEED
PDB

> ALTER SESSION SET CONTAINER=PDB$SEED;
> SELECT name FROM V$DATAFILE;
NAME
--------------------------------------------------------------------------------
/opt/oracle/oradata/CDB/0E6A7D1394775CE6E065000000000001/datafile/o1_mf_system_lspt3n3s_.dbf
/opt/oracle/oradata/CDB/0E6A7D1394775CE6E065000000000001/datafile/o1_mf_sysaux_lspt3pow_.dbf
/opt/oracle/oradata/CDB/0E6A7D1394775CE6E065000000000001/datafile/o1_mf_undotbs1_lspt3qgm_.dbf
```
<br>
Nah, kita sudah tau nih dimana letak directory PDB$SEED-nya. Selanjutnya kita create PDB yang baru menggunakan perintah dibawah.
```
CREATE PLUGGABLE DATABASE pdb2 ADMIN USER adminpdb2 IDENTIFIED BY Itnsa123 ROLES=(dba) FILE_NAME_CONVERT=('/opt/oracle/oradata/CDB/0E6A7D1394775CE6E065000000000001/datafile/','/opt/oracle/oradata/CDB/pdb2/pdb2');
```

### Clone PDB

Show PDB
```
$ sqlplus / as sysdba

SQL> show pdbs

CON_ID      CON_NAME                       OPEN MODE   RESTRICTED
----------- ------------------------------ ----------  ----------
         2  PDB$SEED                       READ ONLY   NO
         3  PDB                            READ WRITE  NO
         4  PDB2                           READ WRITE  NO
```

Now we will change mode PDB to READ ONLY
```
SQL> alter pluggable database PDB close;

Pluggable database altered.

SQL> alter pluggable database PDB open READ ONLY;

Pluggable database altered.

SQL> show pdbs;

CON_ID      CON_NAME                       OPEN MODE     RESTRICTED
----------- ------------------------------ ------------  ----------
         2  PDB$SEED                       READ ONLY     NO
         3  PDB                            READ ONLY     NO
         4  PDB2                           READ WRITE    NO

```

Create PDB3 from PDB
```
SQL>  CREATE PLUGGABLE DATABASE PDB3 FROM PDB CREATE_FILE_DEST='/opt/oracle/oradata';
```

Show PDB
```
SQL> show pdbs;

CON_ID      CON_NAME                   OPEN MODE    RESTRICTED
----------- -------------------------- ------------ ----------
         2  PDB$SEED                   READ ONLY    NO
         3  PDB                        READ ONLY    NO
         4  PDB2                       READ WRITE   NO
         5	PDB3			           MOUNTED      NO
```

Change mode PDB and PDB3 
```
SQL> alter pluggable database pdb close;

Pluggable database altered.

SQL> alter pluggable database pdb open;

Pluggable database altered.

SQL> alter pluggable database PDB3 open;

Pluggable database altered.

```

Show PDB again
```
SQL> show pdbs;

CON_ID      CON_NAME                   OPEN MODE    RESTRICTED
----------- -------------------------- -----------  ----------
         2  PDB$SEED                   READ ONLY    NO
         3  PDB                        READ ONLY    NO
         4  PDB2                       READ WRITE   NO
         5  PDB3	   		           READ WRITE   NO

SQL> select name from v$datafile where con_id=6;

NAME
--------------------------------------------------------------------------------
/opt/oracle/oradata/CDB/0E7A37B2406A3682E065000000000001/datafile/o1_mf_system_lss8t92x_.dbf\
/opt/oracle/oradata/CDB/0E7A37B2406A3682E065000000000001/datafile/o1_mf_sysaux_lss8t92y_.dbf
/opt/oracle/oradata/CDB/0E7A37B2406A3682E065000000000001/datafile/o1_mf_undotbs1_lss8t92y_.dbf

/opt/oracle/oradata/CDB/0E7A37B2406A3682E065000000000001/datafile/o1_mf_users_ls
s8t92y_.dbf
```
