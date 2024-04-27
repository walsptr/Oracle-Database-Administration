# Monitoring using OEM

### Download
download all files from this link
https://www.oracle.com/enterprise-manager/downloads/linux-x86-64-13c-rel5-downloads.html
psatikan semua file dalam 1 direktori yang sama

### Installation
https://oracle-base.com/articles/13c/cloud-control-13cr5-silent-installation-on-oracle-linux-8

```
alter system set "_allow_insert_with_update_check"=true scope=both;
alter system set session_cached_cursors=200 scope=spfile;
alter system set shared_pool_size=600M scope=spfile;
alter system set processes=600 scope=spfile;
shutdown immediate;
startup
show parameter session_cached_cursors
show parameter "_allow_insert_with_update_check"
show parameter shared_pool_size
show parameter processes
```