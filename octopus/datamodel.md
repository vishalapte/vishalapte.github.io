# Octopus

- [Home](index.md)
- **Data Model** 
- [Data Types](datatypes.md) 
- [De-duplication](deduplicate.md) 
- [API](api.md) 

## Data Models

We use two data models to describe all the meta information about a report 
and its columns. This data is used together to
- Fetch raw data
- Deduplicate data
- Return information via API

### DataHeader

``` python
class DataHeader(SpiderModel):
    SOURCES = (
        ('FOO', 'FOO'),
        ('BAR', 'BAR'),
        ('QUX', 'QUX'),
    )

    source = models.CharField(
        choices=Source, max_length=32, 
        default=None, null=True, blank=True, 
    )
    url = models.URLField(default=None, null=True, blank=True, verbose_name='URL')
    title = models.CharField(max_length=256, default=None, null=True, blank=True)
    reportid = models.CharField(max_length=32, default=None, null=True, blank=True)
    is_public = models.BooleanField(default=True)
    is_active = models.BooleanField(default=False)
    frequency = models.IntegerField(default=3600, verbose_name='Frequency')
    filetype = models.CharField(max_length=16, default='zip', null=True, blank=True)
    # deprecated if DataColumn is used correctly
    columns = models.CharField(max_length=2048, default=None, null=True, blank=True)
    # datamodel associated with reportid
    # datamodel is used to store data if not stored as csv file
    datamodel = models.CharField(max_length=128, default=None, null=True, blank=True)
    # require nomenclature to identify filepath of stored csv file
    # if not stored in datamodel
    datastore = models.CharField(max_length=1048, default=None, null=True, blank=True)
    
    class Meta:
        unique_together = (
            ('source', 'reportid')
        )
        verbose_name = 'Dataset'
        verbose_name_plural = 'Datasets'
```

### DataColumn

``` python
class DataColumn(SpiderModel):
    COLTYPE = (
        ('DATETIME', 'Datetime'),
        ('DATE', 'Date'),
        ('TIME', 'Time'),
        ('FILTER', 'Filter'),
        ('SERIES', 'Series')
        ('VALUE', 'Value'),
        ('NOOP', 'NOOP'),
    )
    dataset = models.ForeignKey(DataHeader, on_delete=models.DO_NOTHING)
    colname = models.CharField(max_length=128)
    coltype = models.CharField(choices=COLTYPE, max_length=32, default="SERIES")

    class Meta:
        unique_together = (
            ('dataset', 'colname')
        )
```

### Uniqueness

Uniqueness is a combination of all fields that are

- `DATETIME`
- `DATE`
- `TIME`
- `FILTER`

The following fields do not ever contribute to uniqueness

- `SERIES`
- `VALUE`
- `NOOP`

Uniqueness is applied when de-duplicating data across multiple rows in 
multiple files, and will be applied dynamically by reading metadata 
from the `DataColumn` model.
