# PSQL

In order to login as root user, use the command

``` sql
sudo -u postgres psql
```

In order to clear the session commands, use the command

``` sql
\! clear 
```
for the case of linux

To list the databases post login use the command

``` sql
\l
```

To exit the psql, use the command

``` sql
\q
```

To see the current database selected, use the command

``` sql
select current_database();
```

To check if a sql file is accessbile by a specific user, use the command

``` sql
sudo -u <username> cat <filelocation>
```
filelocation must be full path and not a relative one. If the contents of the file are displayed then yes it's accessible.

To execute a sql script against a database, use the command

``` sql
\i <filelocation>
```
This did not work when the mentioned file was placed in location /user/Documents for the currently logged in user of ubuntu. Instead the file had to be moved to /tmp folder for access.

To see the list of relations in the current database, use the command

``` sql
\dt
```

To create a new database in postgres, use the command

``` sql
create database <db>
```

To select a particular database to work with, use the command

``` sql
\c <db>
```
This will update the prompt with the database name.

To display the relation schema, use the command

``` sql
\d <relation>
```

## Observations

- In the case of creating a relation if we specify the attribute name is uppercase, it is displayed in the relation schema generated as lowercase.
