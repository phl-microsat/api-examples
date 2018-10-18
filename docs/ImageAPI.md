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

### Output
```
{
    "data": [
        {
            "scene_id": "D1_SMI_2018-06-22T053111055_V550",
            "scene_center": {
                "type": "Point",
                "coordinates": [
                    122.43041191598462,
                    13.499050232561672
                ]
            },
            "scene_footprint": {
                "type": "Polygon",
                "coordinates": [
                    [
                        [
                            122.62270772244743,
                            13.438726191427726
                        ],
                        [
                            122.42199776143877,
                            13.303514648530331
                        ],
                        [
                            122.23811610952181,
                            13.559374273695617
                        ],
                        [
                            122.43882607053047,
                            13.694585816593012
                        ],
                        [
                            122.62270772244743,
                            13.438726191427726
                        ]
                    ]
                ]
            },
            "satellite_name": "diwata-1",
            "payload": "smi",
            "cloudcover": null,
            "capture_time": "2018-06-22T05:31:11.055041",
            "wavelength": 550,
            "published_time": null,
            "links": {
                "bundle_url": "https://phl-microsat-storage.dream.upd.edu.ph/images/diwata-1/D1_SMI_2018-06-22T053111055_V550/D1_SMI_2018-06-22T053111055_V550.zip",
                "thumbnail_url": "https://phl-microsat-storage.dream.upd.edu.ph/images/diwata-1/D1_SMI_2018-06-22T053111055_V550/D1_SMI_2018-06-22T053111055_V550-thumb.png"
            },
            "image_quality": null,
            "bands": {
                "L1A": "D1_SMI_2018-06-22T053111055_V550_L1A.tif",
                "L1B": "D1_SMI_2018-06-22T053111055_V550_L1B.tif",
                "L1C": "D1_SMI_2018-06-22T053111055_V550_L1C.tif"
            },
            "day_or_night": "",
            "sun_elevation": 64.52449656078697,
            "sun_azimuth": 296.56580289395646,
            "products": {
                "L1A": "D1_SMI_2018-06-22T053111055_V550_L1A.tif",
                "L1B": "D1_SMI_2018-06-22T053111055_V550_L1B.tif",
                "L1C": "D1_SMI_2018-06-22T053111055_V550_L1C.tif"
            },
            "satellite_color": null,
            "payload_color": null,
            "mission_id": null,
            "mission_name": null,
            "mission_start_time": null
        },

        ...

],
    "meta": {
        "total_count": 1548,
        "total_pages": 154.8,
        "page": 1,
        "page_size": 10
    },
    "links": {
        "histogram": "https://api.orange.phl-microsat.xyz/scenes/histogram?",
        "self": "https://api.orange.phl-microsat.xyz/scenes?page=1&limit=10",
        "first": "https://api.orange.phl-microsat.xyz/scenes?page=1&limit=10",
        "prev": "https://api.orange.phl-microsat.xyz/scenes?page=1&limit=10",
        "next": "https://api.orange.phl-microsat.xyz/scenes?page=2&limit=10",
        "last": "https://api.orange.phl-microsat.xyz/scenes?page=154.8&limit=10"
    }
}
```



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
