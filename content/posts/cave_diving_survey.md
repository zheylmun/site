+++
title = "Cave Diving Survey"
date = "2024-09-17"
updated = "2024-09-17"

[taxonomies]
tags=["Cave Exploration"]
+++

Cave surveys are an essential part of cave diving exploration and documentation.
They provide a detailed map of the cave system which can be used to plan future dives,
identify potential hazards, and document the cave's features.
In order to create accurate and useful surveys, there are several requirements that must be met.
Underwater cave survey poses unique challenges that must be taken into account when planning and conducting survey activities,
as well as when compiling survey data into maps and larger data sets.

## Data Collection

Data collection for underwater cave survey begins on the surface.
The first step is to establish an anchor point for subsequent measurements.
This anchor point acts as the first `station`.
A station is a marked point whose location has been determined as part of a survey.
The anchor point on land would typically be determined with a high-resolution GPS.
With that anchor point taken, the survey begins by measuring a series of `shot`s.
Each shot represents a straight line measurement from the previous station to the next.
It includes a measurement of the heading from one station to the next,
the distance between the stations, as well as the depth at each station.
This allows surveyors to iteratively build a map of where the passages go.
Survey often includes measurements from each station to the surrounding walls.
Including passage measurements provides information about the size and shape of the passages.
Creating detailed maps requires all of the above,
in addition to recording data about the structure of the passages and rooms.
There are a variety of methods for making these measurements,
many of which will be further discussed later in this document.

### Underwater Survey

There are 2 popular kinds of survey in cave diving today.
The first is traditional measurement with a compass, measuring device, and depth gauge.
The second is semi-automated using a handheld measuring device called the [MNemo](https://www.arianesline.com/mnemo/).

Both fundamentally make the same measurements, but the survey and post-processing activities end up being substantially different.

#### Manual Survey

Manual survey involves taking a compass heading, distance, and depth measurement at each station.
The surveyor records these measurements on a slate or waterproof paper.
The surveyor then moves to the next station and repeats the process.
To increase confidence, surveyors may take compass measurements on each side of a station,
giving two measurements of each heading.
This results in a more accurate map, but also requires more time and effort.
Once the dive is complete, the survey data is entered into software and added to a survey project.

#### MNemo Survey

MNemo survey also involves taking a compass heading, distance, and depth measurement at each station,
but the MNemo device takes and records these measurements automatically.
The distance is measured while swimming along the line,
and the compass heading is measured by the orientation of the device.
The depth is measured by the pressure sensor in the device.
Stations are recorded via a simple physical interface,
and the device must be physically attached to the line to record a station.

#### Confounding Factors

Both manual and MNemo survey share a similar set of challenges.

* Measurement Error: All measurements have some degree of error.
  This error can be caused by a variety of factors,
  including human error, equipment error, and environmental conditions.
  In particular, the line used to represent a straight line between stations may stretch,
  or sag, or be affected by currents, which can cause inaccurate distance (and heading) measurements.
* Interference: Compasses can be affected by magnetic interference from metal objects,
  which can cause inaccurate readings.
  This is of particular concern when carrying significant amounts of metal equipment which is unavoidable in cave diving.
* Changing conditions:
  Caves tend to be quite static from a structural perspective,
  but water levels can change, resulting in inconsistent depth measurements.
  In tidal systems, the depth can even change significantly over the course of a single dive.
  This error in particular can be difficult to account for in post-processing.
  Current software packages do not have a good way to account for this particular source of error.

## Survey Data

Cave survey is often done with the intent of creating a map.
Except for tiny caves, the data collection usually requires multiple dives.
In order to accurately combine multiple data collection efforts into a single dataset,
it is important that the data collected is consistent and complete.
This not only includes the measurements taken at each station,
but also the metadata about each activity to enable its proper integration.

### Survey Activity Information

* compass type
* measuring  device
* lrud measurement device
* surveyor
* survey team
* anchor station
* date
* compass cal date
* air temperature
* water temperature
* vis estimate

### Survey Data Items

While there are differences in collection methods, the data collected is fundamentally the same.
The data collected typically includes the following for each `shot`:

| Data Item                   | Mandatory | Description                                                 |
|-----------------------------|-----------|-------------------------------------------------------------|
| From Station                | Yes       | The station the shot is being is being measured from        |
| To Station                  | Yes       | The station the shot is being measured to                   |
| Heading                     | Yes       | The compass heading from the from station to the to station |
| Distance                    | Yes       | The distance between the from station and the to station    |
| Depth                       | Yes       | The depth at the to station                                 |
| Repeat Heading              | No        | A second compass heading taken at the end of the shot       |
| Passage Measurements (LRUD) | No        | Measurements from the station to the passage walls          |
