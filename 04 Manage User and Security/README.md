# Managing Users and Security

### Create Users
```
CREATE USER reader IDENTIFIED BY password DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp ACCOUNT UNLOCK;
CREATE USER author IDENTIFIED BY password DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp ACCOUNT UNLOCK;
```

### Roles
Create Roles
```
CREATE ROLE READ;
CREATE ROLE FULL;
```

grant session
supaya user bisa assigned ke role yang telah dibuat
```
GRANT create session TO READ,FULL;
```

grant privileges to role
```
GRANT select ON tb_test TO READ;
GRANT ALL ON tb_test TO FULL;
```

Grant role to user
```
GRANT READ to reader;
GRANT FULL to author;
```

### Profiles

Create profile
```
CREATE PROFILE pflimit LIMIT
SESSIONS_PER_USER 1
FAILED_LOGIN_ATTEMPTS 2;
```

Create user
```
CREATE USER pfuser IDENTIFIED BY password DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp ACCOUNT UNLOCK;
```

Assigned profile to user
```
ALTER USER pfuser PROFILE pflimit;
```

Checking
```
select profile from dba_users where username = 'pfuser'
```