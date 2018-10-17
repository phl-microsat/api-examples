# GET /scenes
---

### Basic Filters
| **Parameter**            | **Description**                                                                                           | **Example**                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| payload                  | Filter by payload. Sample payloads are: 'hpt', 'smi', 'mfc'. Multiple allowed.                            | `/scenes?payload=smi,hpt`                             |
| satellite_name           | Filter by satellite name. Multiple allowed.                                                               | `/scenes?satellite_name=diwata-1,landsat8`             |
| since                    | Return scenes captured on or after specified date (UTC)                                                   | `/scenes?since=2016-01-01T00:00:00Z`                  |
|                          | Time can be omitted, will default to 00:00:00                                                             | `/scenes?since=2016-01-01`                            |
| until                    | Return scenes captured on or before specified date (UTC)                                                  | `/scenes?until=2016-01-01T00:00:00Z`                  |
|                          | Time can be omitted, will default to 23:59:59 (End of day)                                                | `/scenes?since=2016-01-01`                            |
| cloudcover_min           | Returns scenes with cloudcover percentage greater than or equal to this value.                            | `/scenes?cloudcover_min=5.5`                          |
| cloudcover_max           | Returns scenes with cloudcover percentage less than or equal to this value.                               | `/scenes?cloudcover_max=20.5`                         |
| no_cloudcover           | Returns scenes with or without cloudcover.                                | `/scenes?no_cloudcover=true`                         |
| geo_bounding_box         | Returns scenes that intersect with a bounding box                                                         | `/scenes?geo_bounding_box=118.30078,16.10915,128.6718,9.34067` |
| geo_point                | Returns scenes that encloses a specified pinned point                                                     | `/scenes?geo_point=121.11328,15.05090`                |


### Pagination
By default, the API returns 10 results at a time. Overriding page size and viewing pages can be done using the pagination parameters:

| **Parameter**  | **Description**                         | **Default** | **Example**                                         |
|----------------|-----------------------------------------|-------------|-----------------------------------------------------|
| limit          | The number of items to return per page  | 10          | `/scenes?limit=20`                                  | 
| page           | The page number to view, starts at 1    | 1           | `/scenes?limit=20&page=5`                           | 

### Other Parameters
| **Parameter**  | **Description**                                                      | **Defaults**  | **Example**                                               |
|----------------|----------------------------------------------------------------------|---------------|-----------------------------------------------------------|
| sort           | Sorts results using a field.                                         | -capture_time | `/scenes?sort=payload`                                    |
|                | Multiple sort parameters will prioritize fields from left to right.  |               | `/scenes?sort=payload,capture_time`                       |
|                | Fields can be sorted in descending order by adding a `-` symbol      |               | `/scenes?sort=payload,-capture_time`                      |


# GET /scenes/histogram
This endpoint returns the number of scenes per day. Filters for the `GET /scenes` endpoint also work here!

### Special Parameters
| **Parameter**  | **Description**                                                      | **Defaults**  | **Example**                                               |
|----------------|----------------------------------------------------------------------|---------------|-----------------------------------------------------------|
| bucket_size    | Sets the bucket size (in days) on which to group results             | 1             | `/scenes/histogram?bucket_size=2`                         |
|                | Accepts floats for buckets less than a day wide                      |               | `/scenes/histogram?bucket_size=2.125`                     |



http://localhost:5000/scenes/histogram?since=2016-01-15


# GET /scenes/grids
http://localhost:5000/scenes/geohash?geo_hash_precision=3