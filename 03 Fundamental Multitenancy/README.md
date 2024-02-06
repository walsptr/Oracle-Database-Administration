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