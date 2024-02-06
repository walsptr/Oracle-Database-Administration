# Installing Oracle Database

### Download RPM file oracle database
Download file rpm oracle database melalui link berikut
https://www.oracle.com/cis/database/technologies/oracle19c-linux-downloads.html 

### Preinstall oracle database 19c

Pertama kita akan melakukan preinstall untuk oracle databasenya
```
dnf install oracle-database-preinstall-19c -y
```


### Setup User and Env Oracle
Ganti password user oracle
```
passwd oracle
```
Edit SELINUX menjadi permissive
```
vim /etc/selinux/config

//edit baris perintah dibawah
SELINUX = permissive

//save & quit
setenforce Permissive
```

Setup Environment variable untuk user oracle
```
vim /home/oracle/.bash_profile

export ORACLE_HOME=/opt/oracle/product/19c/dbhome_1
PATH=/opt/oracle/product/19c/dbhome_1/bin:$PATH
```

### Install oracle database 19c
Setelah itu baru kita install file rpm oracle database
```
export CV_ASSUME_DISTID=OEL7.6
dnf localinstall oracle-database-ee-19c-1.0-1.x86_64.rpm  -y
```