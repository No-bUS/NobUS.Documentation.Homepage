---
title: "Backend"
date: 2023-05-17T07:57:01+08:00
draft: false
---

# Backend Overview

The backend plays a crucial role in data processing and serving APIs for the application.

## Technology Stack

To develop the backend, we plan to utilize a combination of Java, Scala, Rust, and C#.

## Services

The NobUS backend will offer a diverse range of services
that can be broadly categorized into two types.

### 1. Static / Informational Services

#### Bus Station List Service

###### Signature

`() => [BusStation]`

###### Description

This service supplies a list of bus stations along with their respective locations.
We may consider making some improvements to the existing `/BusStops` API:

- Eliminate redundant fields, such as ShortName, LongName, name and caption,
  as they often provide duplicate information.
- The inclusion of longitude and latitude may not be necessary for most cases,
  and the frontend can explicitly request them when needed.

#### Bus Route Service

##### Signature

`(BusCode) => [BusRoute]`

##### Description

This supportive service offers information about bus routes.
We can enhance the existing `/ServiceDescription` API by:

- Removing redundant fields, such as `Route` (which holds same value as `RouteLongName`).
- Convert `RouteDescription` to an array.

### 2. Dynamic / Computational Services

#### Bus Arrival Time Service 

##### Signature

`(BusStop, BusCode, TimeStamp=now) => [BusArrivalTime]`

##### Description

This core service provides bus arrival time prediction.
On top of existing ETAs from `/ShuttleService` API,
we would like to add 3 data sources for more accurate estimations:

- Crowd GPS data. By associating user devices with buses and collecting GPS data,
  we can update bus locations more frequently.
- Fixed bus schedule. On weekends, even if buses momentarily disappear from tracking,
  users can still expect a bus to arrive a few minutes after `xx:00` and `xx:30`.
- Historical data. By collecting historical data and employing machine learning techniques,
  we can predict bus arrival times with greater accuracy.

#### Bus Progress Service

##### Signature

`(SourceStation, DestinationStation, Coordinate) => BusProgress`

##### Description

This service provides information on the progress of buses.
It is intended for internal use only.
Instead of directly calling the Google Maps API and obtaining an exact map,
we have opted for a simplified infographic (think about MRT maps).
This simplified abstract map retains the rough shape,
allowing us to represent the progress of a bus using a distance in percentage or meters.
This approach eliminates the need to consult an actual map and simplifies the user experience.
To support this, we require a new service
that can convert coordinates into relative distances or percentages.


#### Bus Location Service

##### Signature

`(BusCode, TimeStamp=now) => [BusLocation]`

##### Description

This service provides real-time bus location information
and will replace the deprecated `/BusLocation` API.

#### Bus Crowd Level Service

##### Signature

`(BusStop, BusCode, TimeStamp=now) => CrowdLevel`

##### Description

This service supplies information on the crowd level of buses.
Although the existing `/ActiveBus` API already provides this data,
we can further enhance its accuracy
by employing mechanisms similar to the bus arrival time prediction service.
