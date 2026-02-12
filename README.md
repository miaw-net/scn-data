# Description
This is the accompanying data set to the following NINeS 2026 publication on Submarine Cable Network (SCN) measurement.
https://nines-conference.org/papers/p016-Weaver.pdf

In this repo you will find a csv file containing information on ~350 submarine cable systems and a folder of .pickle files which contain information for monitoring individual submarine links.

## Terminology

##### Submarine Link (SL)
The set of consecutive hops in a traceroute measurement that cross the ocean and use submarine infrastructure.

##### Segment
Submarine Cable Systems oftentimes have > 2 landing points and are comprised of segments -- this is the portion of a cable system that lies between two directly connected landing points.

##### Landing Point (LP)
A landing point is the location where the submarine cable emerges from the water and connects to terrestrial infrastructure.

##### Submarine Cable Operators
Entity that owns or maintains submarine cables. May or may not also directly use the cable to route traffic.

##### Submarine Cable Users
Entities that purchase capacity on submarine cables.

##### Vantage Point (VP)
A measurement node in the Internet used to launch measurements. For this work, we look at traceroute measurements.

##### RIPE Atlas Anchor
RIPE Atlas is a global network of devices that measure the Internet. We use RIPE Atlas anchors (https://atlas.ripe.net/anchors/list) as our measurement vantage points in this study. These anchors run full mesh measurements at a rate of approx. once every fifteen minutes. Due to the wide geographic spread of anchors, many of these measurements cross submarine infrastructure. Anchors can be identified by their probe ID (ex: https://atlas.ripe.net/probes/6647/overview). There is a RIPE Atlas API and Python wrapper that you can use to pull probe and measurement data (https://ripe-atlas-cousteau.readthedocs.io/en/latest/). 

## cable_systems.csv
This file contains information on ~350 submarine cable systems. There are still blank rows in the data set containing the names of submarine cable systems that's data has yet to be added. These empty rows are placeholders for future expansion of the data set.

## SL_endpoints
This folder contains the RIPE Atlas anchor probe IDs and submarine link IP addresses identified during the course of this study. We are making it available for others who may be interested in running measurements over submarine cables. This folder contains a set of subfolders named after cable systems. In each subfolder are a set of pickle files named after specific cable segments. 
Inside each pickle file, you will find a list of probe pairs whose measurements cross a specific submarine cable segment and the IP addresses that we mapped to that cable segment. We verify that these IP addresses correspond to a submarine cable system by using the IP geolocation and AS inference techniques detailed in section 3 of our paper.

###### Example: aec-1/Holyhead,United_Kingdom/Shirley,US.pickle

<sub>You can read this file as a dictionary. It has two keys, 'forward_data' and 'reverse_data.' Each leads to its own sub-dictionary which stores 'probe_pairs' and 'SL_endpoints.'</sub>

- <sub><strong>forward_data</strong> : Information on monitoring the segment in the direction GB to the US.</sub>

- <sub><strong>reverse_data</strong> : Information on monitoring the segment in the direction the US to GB.</sub>

- <sub><strong>probe_pairs</strong>  : List of RIPE Atlas anchors wherein measurements between these anchors cross the target submarine segment.

- <sub><strong>SL_endpoints</strong> : List of pairs of consecutive IP addresses crossing submarine infrastructure in traceroutes between the probe pairs.


## Disclaimer
IP assignments do change over time, as do routes in the Internet. This study was conducted using traceroute measurements from December 2024, so looking for the same IP addresses from the same probes may yield different results if you are considering measurements in a different time frame.

Untangling submarine cables from traceroute measurements is difficult. Multiple submarine cable systems may have overlapping landing point locations and known users, making discerning the true underlying infrastructure from traceroute measurements near impossible, as geolocation and AS inference from submarine link IP addresses is not sufficient. This is particularly true for large cable systems in East Asia and crossing the Suez Canal. In cases of ambiguity, we are able to verify that submarine infrastructure is being crossed, though the confidence in mapping is decreased. For more information on how we this ambiguity, please check out section 3 of our paper.

## Contact
Please reach out to mweaver6@wisc.edu with any questions or collaboration ideas. Happy measuring!
