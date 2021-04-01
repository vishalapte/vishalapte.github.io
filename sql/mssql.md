## Microsoft SQL Server

### Running queries

```sql
1> SQL_QUERY;
2> GO
```

### DELETE ALL Records

```sql
TRUNCATE TABLE mytable
```

### RESET AUTOINCREMENT

```sql
DBCC CHECKIDENT (mytable, RESEED, 0)
```
