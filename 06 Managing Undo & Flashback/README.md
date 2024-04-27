# Undo & Flashback

## Undo

```
ROLLBACK;
```

## Fast Recovery Area
### Check directory FRA
```
select * from v$recovery_file_dest;
```
```
show parameter recovery;
```

### Enable fast recovery area
```
alter system set db_recovery_file_dest_size=20G scope=both;
alter system set db_recovery_file_dest='/opt/oracle/oradata/oradb/fra' scope=both;
```

## Archivelog mode
### Check archive log mode
```
SELECT LOG_MODE FROM V$DATABASE;
```

### Enable archive log mode
```
SHUTDOWN IMMEDIATE;
STARTUP MOUNT;
ALTER SYSTEM SET LOG_ARCHIVE_DEST_1 = 'LOCATION=USE_DB_RECOVERY_FILE_DEST' scope=both;;
ALTER DATABASE ARCHIVELOG;
ALTER DATABASE OPEN;
```

## Flashback
### Check flashback
```
SELECT FLASHBACK_ON FROM V$DATABASE;
```

### Enable flashback
```
ALTER SYSTEM SET DB_FLASHBACK_RETENTION_TARGET=4320;
ALTER DATABASE FLASHBACK ON;
```

### Create normal restore point
```
create restore point normal_rs;
```

do some changes on database

### Do flashback
```
startup mount;
flashback database to restore point guaran_rs;
alter database open resetlogs;
```

### Create guaranteed restore point
```
create restore point guaran_rs guarantee flashback database;
```

do some changes on database

### Do flashback
```
startup mount;
flashback database to restore point guaran_rs;
alter database open resetlogs;
```

### checking name restore point
```
select * from v$restore_point;
```

### Delete restore point
```
DROP RESTORE POINT name_restore_point;
```