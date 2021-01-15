# Octopus

- [Home](index.md)
- [Data Model](datamodel.md) 
- **Data Types**
- [De-duplication](deduplicate.md) 
- [API](api.md) 

## Types of data

### Data Type A

#### Sample Data

| IntervalEnding     | North   | South  | East   | West   | Model | InUseFlag | DSTFlag |
|--------------------|--------:|-------:|-------:|-------:|:-----:|:---------:|:-------:|
| `12/16/2020 07:15` | `12692` | `2139` | `4078` | `1233` | `E`   |    `Y`    |   `N`   |
| `12/16/2020 07:15` | `12706` | `3123` | `5123` | `1243` | `A6`  |    `N`    |   `N`   |
| `12/16/2020 07:20` | `24132` | `4123` | `4123` | `1412` | `E`   |    `Y`    |   `N`   |

#### DataColumn Mapping

DATETIME
- INTERVALENDING: DATETIME

FILTER
- MODEL: FILTER
- INUSEFLAG: FILTER
- DSTFLAG: FILTER

SERIES/VALUE
- NORTH: SERIES
- SOUTH: SERIES
- EAST: SERIES
- WEST: SERIES

#### Uniqueness

- INTERVALENDING
- MODEL
- INUSEFLAG
- DSTFLAG

### Data Type B

#### Sample Data

| IntervalEnding     | Region    | Value       | Model | InUseFlag | DSTFlag |
|--------------------|-----------|------------:|:-----:|:---------:|:-------:|
| `12/22/2020 00:10` |  `NORTH`  | `1453.5999` |  `A`  |    `Y`    |   `N`   |
| `12/22/2020 00:10` |  `NORTH`  | `1400.4100` |  `B`  |    `N`    |   `N`   |
| `12/22/2020 00:10` |  `SOUTH`  | `1057.9000` |  `A`  |    `Y`    |   `N`   |
| `12/22/2020 00:10` |  `SOUTH`  | `1031.9000` |  `B`  |    `N`    |   `N`   |

#### DataColumn Mapping

DATETIME
- INTERVALENDING: DATETIME

FILTER
- REGION: FILTER
- MODEL: FILTER
- INUSEFLAG: FILTER
- DSTFLAG: FILTER

SERIES/VALUE
- VALUE: VALUE

#### Uniqueness

- INTERVALENDING
- REGION
- MODEL
