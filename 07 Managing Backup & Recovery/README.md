# Backup and Recovery

## Full Backup
### Backup database plus archivelog
```
rman target=/
backup database plus archivelog;
```

if you get error like this
```
ORA-19804: cannot reclaim **bytes disk space from** bytes limit
```

just delete archivelog
```
delete archivelog all completed before 'sysdate-1';
```

### Backup database root container
```
backup database root;
```

### Backup pluggable database
```
backup pluggable database <nama-pdb>;
```

### Backup database with tag
```
backup database tag 'backup-1';
```

## Incremental Backup
### Incremental backup plus archive log

level 0 backup
```
backup incremental level 0 database tag 'backup-level0' plus archivelog;
```

level 1 differential backup
```
backup incremental level 1 database tag 'backup-level1' plus archivelog;
```

level 1 cumulative backup
```
backup incremental level 1 cumulative database tag 'backup-level1' plus archivelog;
```

best practice backup
https://docs.google.com/document/d/1OtqdzxJgGe5h5Wo3XjubUV64TyS0f3HlO9hB27hkom4/edit

### list backup
```
list backup;
list backup summary;
```