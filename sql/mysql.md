# MySQL

## Getting Started

Know values for the following variables

- `dbname`
- `dbuser`
- `simple_password`
- `secure_password`

## Configure user and database

```sql
FLUSH PRIVILEGES;

CREATE DATABASE IF NOT EXISTS <dbname>;

CREATE USER IF NOT EXISTS 'dbuser'@'localhost' IDENTIFIED BY 'simple_password';
ALTER USER 'dbuser'@'localhost' IDENTIFIED BY 'secure_password';
GRANT ALL ON dbname.* to 'dbuser'@'localhost';

FLUSH PRIVILEGES;
```

## Review

```sql
SHOW GRANTS FOR 'dbuser'@'localhost';
```
