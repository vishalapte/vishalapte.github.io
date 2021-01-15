# Octopus

- [Home](index.md)
- [Data Model](datamodel.md) 
- [Data Types](datatypes.md) 
- [De-duplication](deduplicate.md) 
- **API** 

## API

### `/spider/report/<report_id>/`

Metadata about every report

### `/spider/report/<report_id>/column/<column_name>/`

Return a list of all unique values for the column if `coltype = FILTER`

### `/spider/report/<report_id>/data/`

ALL downloaded data for a given report

### `/spider/report/<report_id>/data/?\<filter_column\>=\<value\>&series=\<series_column\>`

Search dataset by series and/or for all rows where filter_column equal to value
