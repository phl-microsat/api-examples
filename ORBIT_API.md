## I. TLE
#### `/v1/tle/<catalog_id>/<timestamp>`
Computes for a Satellite's latest TLE at a given timestamp.

| **Parameter**            | **Description**                                                                                           | **Example**                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| catalog_id               | The satellite's NORAD Catalog ID                                                                          | `/v1/tle/25544`                                       |
| timestamp                | The query time in `YYYYMMDDTHHmmSS` format. (Optional) endpoint will return latest available tle if not indicated  | `/v1/tle/25544/20160101T000000Z`             |

#### Output
```
{
  "meta": {
    "query_time": "2017-03-01T20:02:03Z",
    "catalog_id": 41463
  },
  "data": {
    "epoch": "2017-03-01T10:15:40Z",
    "line2": "2 41463  51.6401 208.3272 0001265 113.8349 280.7374 15.60239226 47967",
    "line1": "1 41463U 98067HT  17060.42754914  .00009770  00000-0  12352-3 0  9997"
  }
}
```

---

## II. POINT
#### `/v1/point/<catalog_id>/<timestamp>`

Computes for a Satellite's location at a given timestamp.

| **Parameter**            | **Description**                                                                                           | **Example**                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| catalog_id               | The satellite's NORAD Catalog ID                                                                          | `/v1/point/25544`                                     |
| timestamp                | The query time in `YYYYMMDDTHHmmSS` format. (Optional) endpoint will return location at current time if not indicated  | `/v1/point/25544/20160101T000000Z`       |

#### Output
```
{
  "meta": {
    "tle": {
      "epoch": "2017-03-01T10:15:40Z",
      "query_time": "2017-03-01T20:02:29Z",
      "catalog_id": 41463,
      "line1": "1 41463U 98067HT  17060.42754914  .00009770  00000-0  12352-3 0  9997",
      "line2": "2 41463  51.6401 208.3272 0001265 113.8349 280.7374 15.60239226 47967"
    }
  },
  "data": {
    "geometry": {
      "type": "Point",
      "coordinates": [
        -83.50029886764565,
        11.579648294293035
      ]
    },
    "type": "Feature",
    "properties": {
      "timestamp": 1488398549.520333,
      "elevation": 386364.625
    }
  }
}
```

--- 
## III. TRACK
#### `/v1/track/<catalog_id>/<start_time>/<end_time>`
Generates a ground track of a satellite for a time range

| **Parameter**            | **Description**                                                                                           | **Example**                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| catalog_id               | The satellite's NORAD Catalog ID                                                                          | `/v1/track/41463/20160617T012441Z/20160617T013033Z`   |
| start_time               | The start time for the simulation in `YYYYMMDDTHHmmSS` format.                                            | `/v1/track/41463/20160617T012441Z/20160617T013033Z`   |
| end_time                 | The end time for the simulation in `YYYYMMDDTHHmmSS` format.                                              | `/v1/track/41463/20160617T012441Z/20160617T013033Z`   |

#### Output
```
{
  "data": {
    "type": "FeatureCollection",
    "features": [
      {
        "geometry": {
          "type": "Point",
          "coordinates": [
            128.5868625223309,
            -3.7603013102821055
          ]
        },
        "type": "Feature",
        "properties": {
          "timestamp": 1466126681,
          "elevation": 402161.75
        }
      },
      ...
    ]
  },

  "meta": {
    "start_time": "2016-06-17T01:24:41Z",
    "time_computed": "2017-03-01T19:48:52Z",
    "tle": {
      "epoch": "2016-06-16T22:43:38Z",
      "line2": "2 41463 051.6437 059.0374 0000484 137.3380 311.2883 15.55536957007829",
      "line1": "1 41463U 98067HT  16168.94697410 +.00008216 +00000-0 +12472-3 0  9996",
      "catalog_id": 41463
    },
    "end_time": "2016-06-17T01:30:33Z"
  },
}
```

---

## IV. PASSES
#### `/v1/passes/<catalog_id>`
| **Parameter**            | **Description**                                                                                           | **Example**                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| catalog_id               | The satellite's NORAD Catalog ID                                                                          | `/v1/passes/41463`   |
| lon                      | The longitude of the observer                                                                             | `/v1/passes/41463?lon=121.071999&lat=14.647318&alt=77`   |
| lat                      | The latitude of the observer                                                                              | `/v1/passes/41463?lon=121.071999&lat=14.647318&alt=77`   |
| alt                      | The altitude of the observer                                                                              | `/v1/passes/41463?lon=121.071999&lat=14.647318&alt=77`   |
| horizon                  | The minimum degress from horizon to include in the pass. (Optional) Defaults to 5                | `/v1/passes/41463?lon=121.071999&lat=14.647318&alt=77&horizon=10` |

#### Output

```
{
  "data": [
    {

      # Details on the pass including points from 0 deg horizon
      "horizon_pass": {
        "duration": 549,
        "set_time": "2017-03-02T05:17:25Z",
        "rise_time": "2017-03-02T05:08:15Z",
        "ground_track_link": "http://localhost:5000/v1/track/41463/20170302T050815Z/20170302T051725Z"
      },

      # Details are available if the satellite gets eclipsed by the earth's shadow during the pass
      "eclipse": {
        "before_aos": false,
        "on_los": false,
        "end": null,
        "start": null
      },

      # Details on the pass based on the given horizon value
      "pass": {
        "max_altitude_time": "2017-03-02T05:12:51Z",
        "rise_azimuth": 0.1943311244249344,
        "duration": 229,
        "set_time": "2017-03-02T05:14:45Z",
        "max_altitude": 0.2615211009979248,
        "rise_time": "2017-03-02T05:10:56Z",
        "ground_track_link": "http://localhost:5000/v1/track/41463/20170302T051056Z/20170302T051445Z",
        "set_azimuth": 1.5107674598693848
      }
    },
    ...
  ],

  "meta": {
    "observer": {
      "lat": 14.647318,
      "alt": 77,
      "lon": 121.071999
    },
    "horizon": "10",
    "time_computed": "2017-03-01T19:57:07Z",
    "tle": [
      "1 41463U 98067HT  17060.42754914  .00009770  00000-0  12352-3 0  9997",
      "2 41463  51.6401 208.3272 0001265 113.8349 280.7374 15.60239226 47967"
    ],
    "days": 2
  }
}
```