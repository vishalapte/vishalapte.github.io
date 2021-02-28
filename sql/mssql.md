## Microsoft SQL Server

### Running queries

```
1> SQL_QUERY;
2> GO
```

### DELETE ALL Records

```
TRUNCATE TABLE mytable
```

### RESET AUTOINCREMENT

```
DBCC CHECKIDENT (mytable, RESEED, 0)
```
