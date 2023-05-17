---
title: "On Official NUSNextBUS API"
date: 2023-05-16T23:53:39+08:00
draft: false
---

# Current Issues

## Redundant Fields


The `/BusStops` endpoint returns a list of bus stations.
Each station has four fields for its name:
`LongName`, `ShortName`, `Caption` and `name`.
However, these fields are often redundant.
For example, `LongName` and `Caption` usually have the same value,
and`ShortName` and `name` only differ slightly.
Here is a sample of the JSON response:
```json

[
  {
    "caption": "Prince George's Park",
    "name": "PGP",
    "LongName": "Prince George's Park",
    "ShortName": "PGP",
    "latitude": 1.291765,
    "longitude": 103.780419
  },
  {
        "caption": "Kent Ridge MRT",
        "name": "KR-MRT",
        "LongName": "Kent Ridge MRT",
        "ShortName": "KR MRT",
        "latitude": 1.29483,
        "longitude": 103.784439
  }
]
```

## Incorrect Data Type

The `/BusStops` endpoint returns the list of bus stations in JSON format,
but the response header specifies the data type as `text/html`.
This can cause problems for clients.

## Inconsistent Naming Conventions

The fields and endpoints use different naming conventions,
which can be confusing and inconsistent.
For instance, the `name` field is in lower case,
while the `LongName` field is in PascalCase.
Similarly, the `/publicity` endpoint is in lower case,
while the `/BusStops` endpoint is in PascalCase.
A more consistent naming convention would,
definitely, improve the readability and usability of the API.