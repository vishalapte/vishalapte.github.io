# Octopus

- [Home](index.md)
- [Data Model](datamodel.md) 
- [Data Types](datatypes.md) 
- [De-duplication](deduplicate.md) 
- **API** 

## API

ALL API calls support the `format` param, regardless of whether by `GET` or `POST`.

### `/spider/report/`

List of all reports descrbed in DataHeader.

Support:
- `GET`, `POST`
- `format=[html|json|csv]` 
- Default: `format=html`

### `/spider/report/<source>/`

List of all reports described in DataHeader for given `<source>`

Support:
- `GET`, `POST`
- `format=[html|json|csv]` 
- Default: `format=html`

### `/spider/report/<source>/<report_id>/`

Support:
- `GET`, `POST`
- `format=[html|json|csv]` 
- Default: `format=html`

Metadata about every report

- ReportID
- Title
- List of columns grouped by column type
- List of all downloaded files and chart showing timeline of when file was downloaded

### `/spider/report/<source>/<report_id>/column/`

Support:
- `GET`, `POST`
- `format=[html|json|csv]` 
- Default: `format=html`

Return a list of all columns and coltype and any other metadata about column defined in the datamodel.

### `/spider/report/<source>/<report_id>/column/<colname>/`

Support:
- `GET`, `POST`
- `format=[html|json|csv]` 
- Default: `format=html`

Return a list of all unique values for the column if
- `column_name` in list of mapped columns
- `coltype` = `FILTER`

### `/spider/report/<source>/<report_id>/data/`

Support:
- `GET`, `POST`
- `format=[html|json|csv]`
- Default: `format=json`

Return all downloaded data for a given report. Supported GET/POST params, in order of priority:
1. `series=<colname>`
2. `colname=<filter_value>`
3. `start=<YYYY-MM-DD>`: inclusive of value (greater than or equal to)
4. `end=<YYYY-MM-DD>`: inclusive of value (less than or equal to)
5. `lastn=<int>`
6. `lastndays=<int>`
7. `format=[json|csv]`

#### param: `series`

- `colname` must be defined in DataColumn
- `colname` must have coltype=SERIES
- Support for list of values... `series=colname_a,colname_b,colname_c`
- Results are returned for all valid values of series. Invalid names are ignored.

#### param: `colname`

- `colname` must be defined in DataColumn 
- `colname` must have coltype=FILTER
- Support for list of values... `colname=colname_a,colname_b,colname_c`
- Results are returned for all valid values of colname. Invalid names are ignored.
