# CU-Hack Night Voting History Warehouse
This project implements a dimensional data warehouse for voting behavior for
Champaign county voters. It creates a warehouse of voting information that
reports every voter who participated in an election and keeps track
of how old they are, gender, where they are registered and where (and when)
they voted.

For more information, please come to [CU Hack Night](https://cuhacknight.org/)

## Setup Instructions
1. I created a postgres database and installed postgis additions
2. Ran DDL from src/main/sql to create tables and insert static data
2. There is an insert in the static data file that creates the spatial reference for East Illinois
```INSERT into spatial_ref_sys (srid, auth_name, auth_srid, proj4text, srtext) values ( 102671, 'esri', 102671, '+proj=tmerc +lat_0=36.66666666666666 +lon_0=-88.33333333333333 +k=0.9999749999999999 +x_0=300000 +y_0=0 +ellps=GRS80 +datum=NAD83 +to_meter=0.3048006096012192 +no_defs ', 'PROJCS["NAD_1983_StatePlane_Illinois_East_FIPS_1201_Feet",GEOGCS["GCS_North_American_1983",DATUM["North_American_Datum_1983",SPHEROID["GRS_1980",6378137,298.257222101]],PRIMEM["Greenwich",0],UNIT["Degree",0.017453292519943295]],PROJECTION["Transverse_Mercator"],PARAMETER["False_Easting",984249.9999999999],PARAMETER["False_Northing",0],PARAMETER["Central_Meridian",-88.33333333333333],PARAMETER["Scale_Factor",0.999975],PARAMETER["Latitude_Of_Origin",36.66666666666666],UNIT["Foot_US",0.30480060960121924],AUTHORITY["EPSG","102671"]]');```
3. I used shp2pgsql to import the shapefiles into the db using 102671 as the srid
4. Ran `src\main\pdi\LoadElectionDayVotingRecords.ktr` to load data into the warehouse.
5. Then `src\main\pdi\LoadAbsenteeVotingRecords.ktr` to load the remaining data
