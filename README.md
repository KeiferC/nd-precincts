# North Dakota Precincts Geodata

## Sources

#### `geodata/nd_blocks_shp_nhgis.zip`
Shapefile of 2010 North Dakota Census Blocks

- __Retrieved:__ June 2020 from the [National Historical Geographic Information System (NHGIS) database](https://data2.nhgis.org/)

- __Usage:__ Joined with `geodata/nd_blocks_tab_nhgis.zip` to embed tabular demographics data into geographic data


#### `geodata/nd_blocks_shp_tl.zip`
Shapefile of the 2010 North Dakota Census Blocks

- __Retrieved:__ June 2020 from the 2019 collection of the
[US Census Bureau's TIGER/LINE database](https://www.census.gov/cgi-bin/geo/shapefiles/index.php)

- __Usage:__ Individual blocks were merged to digitally draw topographically-sound precinct boundaries based on raster maps.

#### `geodata/nd_blocks_tab_nhgis.zip`
Tabular demographics data of the 2010 North Dakota Census Blocks

- __Retrieved:__ June 2020 from the [NHGIS database](https://data2.nhgis.org/)

- __Usage:__ Joined with `geodata/nd_blocks_shp_nhgis.zip` to embed tabular demographics data into geographic data

#### `geodata/nd_counties_shp.zip`
Shapefile of North Dakota Counties as drawn in 2019

- __Retrieved:__ June 2020 from the 2019 collection of the [TIGER/LINE database](https://www.census.gov/cgi-bin/geo/shapefiles/index.php)

- __Usage:__ Used to outline county boundaries for the purposes of digitizing raster maps

#### `geodata/nd_precincts_pres16_tab_medsl.xlsx`
Tabular precinct-level 2016 US Presidential General Election data

- __Retrieved:__ June 2020 from the [MIT Election Data and Science Lab (MEDSL) database](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/LYWX3D)

- __Usage:__ Queried with `‘state_postal = ND’` to extract North Dakota 2016 US Presidential General Election data at the precinct level in order to join with counties' precinct geographic data


### Barnes County (`counties/barnes/`)

#### `raw/1-barnes-county.jpg` & `2-valley-city.jpg`
Barnes County precinct maps

- __Retrieved:__ June 2020 from the [Barnes County website](http://www.co.barnes.nd.us/commission/DistrictMaps/)

- __Usage:__ Georeferenced in [QGIS](https://www.qgis.org/en/site/) with [OpenStreetMap (OSM)](https://www.openstreetmap.org/#map=4/38.01/-95.84) and digitized using TIGER/LINE census blocks shapefiles

#### County Auditor Contact Info

- __Name:__ Beth M Didier

- __Phone:__ (701) 845-8500 Ext. 6666

- __Fax:__ (701) 845-8548

- __Email:__ bdidier@barnescounty.us

- __Address:__ 230 4th St NW Room 202. Valley City, ND 58072-2947


## Data Processing

### Barnes County (`counties/barnes/`)

#### County Metadata
Number of precincts and precinct names were retrieved June 2020 from the [North Dakota Secretary of State Election Results database](https://vip.sos.nd.gov/PortalListDetails.aspx?ptlhPKID=62&ptlPKID=4)

#### Digitization of Precinct Maps
Raster maps from the county's website were georeferenced in QGIS and then
used to outline precinct boundaries around which census blocks were geographically merged. All maps were projected in `EPSG:26914` (NAD83/UTM zone 14N)

#### Precinct Matching
Precinct name matching was done by geographically finding addresses within
precinct boundaries using a combination of [Google Maps](https://maps.google.com) and QGIS, and by looking up the precinct names using the [Election District Lookup function on the North Dakota Secretary of State Website](https://vip.sos.nd.gov/WhereToVote.aspx?tab=ElectionDistricts&ptlPKID=&ptlhPKID=)

#### Data Joining
Shapefile and tabular data joins were done using python. The documented script can be found in the Jupyter Notebook `barnes-join-maup.ipnyb`

#### GeoData Aggregation
Census-block-level demographics geodata were aggregated into precinct-level election geodata using the python `maup` package. The documented script can be found in the Jupyter Notebook `barnes-join-maup.ipnyb` 


## Results

### Barnes County (`counties/barnes/`)

#### `barnes_county.zip`

A precinct-level shapefile of Barnes county containing demographics data (as collected from the 2010 US census) and election data from the 2016 United States Presidential General Election. 

> Note: The shapefile does not contain Census-block-group-level data, which contains citizenship data. The shapefile only contains demographics data of residents aged 18 or older (voting age population (VAP)). Because of the immigration history and the election requirements of the United States, not all in the Hispanic voting age population (HVAP) nor all in the Asian voting age population (ASIANVAP) are citizens. Consequentially, not all in the HVAP nor in the ASIANVAP are permitted to vote in United States federal elections. Therefore, any ecological regression (ER) or ecological inference (EI) analyses using HVAP or ASIANVAP lack statistical accuracy.

#### Analysis

Coming soon...

## Naming Reference

The columns names used in the geodata follow the [Metric Geometry and Gerrymandering Group (MGGG)](https://mggg.org) naming conventions.

### Election Data

- `PRES16D`: Votes for the Democratic candidate in the 2016 United States Presidential General Election

- `PRES16R`: Votes for the Republican candidate in the 2016 United States Presidential General Election

- `PRES16L`: Votes for the Libertarian candidate in the 2016 United States Presidential General Election

- `PRES16G`: Votes for the Green candidate in the 2016 United States Presidential General Election

### Demographics Data

#### Population Data 

- `TOTPOP` (H7Z001): Total population

- `NH_WHITE` (H7Z003): White, non-Hispanic alone population

- `NH_BLACK` (H7Z004): Black, non-Hispanic alone population

- `NH_AMIN` (H7Z005): American Indian and Alaska Native, non-Hispanic alone population

- `NH_ASIAN` (H7Z006): Asian, non-Hispanic alone population

- `NH_NHPI` (H7Z007): Native Hawaiian and Pacific Islander, non-Hispanic alone population

- `NH_OTHER` (H7Z008): Other race, non-Hispanic alone population

- `NH_2MORE` (H7Z009): Non-Hispanic population of two or more races

- `HISP` (H7Z010): Total Hispanic/Latino population

- `H_WHITE` (H7Z011): White, Hispanic alone population

- `H_BLACK` (H7Z012): Black, Hispanic alone population

- `H_AMIN` (H7Z013): American Indian and Alaska Native, Hispanic alone population

- `H_ASIAN` (H7Z014): Asian, Hispanic alone population

- `H_NHPI` (H7Z015): Native Hawaiian and Pacific Islander, Hispanic alone population

- `H_OTHER` (H7Z016): Other race, Hispanic alone population

- `H_2MORE` (H7Z017): Hispanic population of two or more races

#### Voting Age Population (VAP) Data

- `VAP` (H75001): Total voting age population

- `HVAP` (H75002): Hispanic voting age population

- `WVAP` (H75005): White, non-Hispanic voting age population

- `BVAP` (H75006): Black, non-Hispanic voting age population

- `AMINVAP` (H75007): American Indian and Alaska Native, non-Hispanic voting age population

- `ASIANVAP` (H75008): Asian, non-Hispanic voting age population

- `NHPIVAP` (H75009): Native Hawaiian and Pacific Islander, non-Hispanic voting age population

- `OTHERVAP` (H75010): Other race, non-Hispanic voting age population

- `2MOREVAP` (H75011): Voting age population of two or more races


