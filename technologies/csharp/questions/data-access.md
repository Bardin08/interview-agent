# Data Access
<!-- File: interview-agent/technologies/csharp/questions/data-access.md -->

## Topic Overview
ADO.NET, Entity Framework, Entity Framework Core, Dapper, and database patterns.

**Weight**: 1.1

---

## Questions

### Difference between DataTable and DataReader
- **DataTable**: In-memory representation, disconnected, supports random access
- **DataReader**: Forward-only, read-only, connected, better performance for large datasets

### How to loop through all rows of a DataTable?

**ForEach loop:**
```csharp
foreach (DataRow row in dTable.Rows)
{
    yourvariable = row["ColumnName"].ToString();
}
```

**For loop:**
```csharp
for (int j = 0; j < dTable.Rows.Count; j++)
{
    yourvariable = dTable.Rows[j]["ColumnName"].ToString();
}
```
