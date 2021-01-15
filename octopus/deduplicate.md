# Octopus

- [Home](index.md)
- [Data Model](datamodel.md) 
- [Data Types](datatypes.md) 
- **De-duplication** 
- [API](api.md) 

## De-duplication

Data is often published in rolling periods. This means that the last nth 
records are published every x intervals. In this case, the application has
to combine every rolling dataset into one single data set.

### Raw Data

File 1 has a timestamp of 12/18/2020 05:40

| IntervalEnding     | Total  | DSTFlag |
|--------------------|-------:|:-------:|
| `12/18/2020 05:40` | `0.10` |   `N`   |
| `12/18/2020 05:45` | `0.20` |   `N`   |
| `12/18/2020 05:50` | `0.30` |   `N`   |
| `12/18/2020 05:55` | `0.40` |   `N`   |
| `12/18/2020 06:00` | `0.50` |   `N`   |
| `12/18/2020 06:05` | `0.60` |   `N`   |

File 2 has a timestamp of 12/18/2020 05:35

| IntervalEnding     | Total  | DSTFlag |
|--------------------|-------:|:-------:|
| `12/18/2020 05:35` | `0.11` |   `N`   |
| `12/18/2020 05:40` | `0.21` |   `N`   |
| `12/18/2020 05:45` | `0.31` |   `N`   |
| `12/18/2020 05:50` | `0.41` |   `N`   |
| `12/18/2020 05:55` | `0.51` |   `N`   |
| `12/18/2020 06:00` | `0.61` |   `N`   |

File 3 has a timestamp of 12/18/2020 05:30

| IntervalEnding     | Total  | DSTFlag |
|--------------------|-------:|:-------:|
| `12/18/2020 05:30` | `0.15` |   `N`   |
| `12/18/2020 05:35` | `0.25` |   `N`   |
| `12/18/2020 05:40` | `0.35` |   `N`   |
| `12/18/2020 05:45` | `0.45` |   `N`   |
| `12/18/2020 05:50` | `0.55` |   `N`   |
| `12/18/2020 05:55` | `0.65` |   `N`   |

### Combined File

- Most recent data gets priority over older data.
- We want the provenance of each merged row. All de-duplicated data has 
  an additional system generated column that identifies the dataset that
  was used in the de-duplicated row

| DataTimestamp      | IntervalEnding     | Total  | DSTFlag |
|--------------------|--------------------|-------:|:-------:|
| `12/18/2020 05:30` | `12/18/2020 05:30` | `0.15` |   `N`   |
| `12/18/2020 05:35` | `12/18/2020 05:35` | `0.11` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 05:40` | `0.10` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 05:40` | `0.20` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 05:50` | `0.30` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 05:55` | `0.40` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 06:00` | `0.50` |   `N`   |
| `12/18/2020 05:40` | `12/18/2020 06:05` | `0.60` |   `N`   |

