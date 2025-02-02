# Openspoor

![alt text](https://www.radingspoor.nl/images/Stoom/Modellen_van_Leden/7_Inch_modellen/Zandloc_Janny/51133945_533417650499237_1555124498724814848_n.jpg)

The openspoor package is intended to allow easy transformation between different geographical and topological systems 
commonly used in Dutch Railway. Its goal is to be publicly available and function as an open source package.

Currently the openspoor package allows the following transformations:

**Type of input:**
- Point data

These transformations can be performed between the following systems:

**Geographical systems:**
- WGS84 coordinate system (commonly known as GPS coordinates)
- EPSG:28992 coordinate system (commonly known in the Netherlands as Rijksdriehoek)

**Topological systems:**
- Geocode and geocode kilometrering
- Spoortak and spoortak kilometrering (unavailable on switches)

## Getting Started

#### Installation
Installation using anaconda
- Clone the "openspoor" repository
  - `pip install openspoor`
- create an environment:
  - `conda create -n openspoorenv python==3.6.12`
- activate the environment:
  - `conda activate openspoorenv`
- If you are installing on **Windows OS** with Anaconda, first install rtree and geopandas through anaconda with the commands: 
  - `conda install rtree==0.8.3 -y`
  - `conda install geopandas==0.6.1 -y`
- In the root directory of the repository, execute the command:
  - `pip install -r requirements.txt`
- In the root directory of the repository, execute the command:
  - `pip install .`
- In the root directory of the repository, execute the command: 
  - `python -m pytest`
- If all the test succeed, the openspoor package is ready to use and you are on the right "track"!

#### Demonstration notebook

In the future a notebook will be added that demonstrates the use of the openspoor package. For now one can take the 
code in the acceptance tests as example of how to use the package.

## Dependencies

The transformations available in the openspoor package rely completely on data and API's made available at 
https://mapservices.prorail.nl/. Be aware of this dependency and specifically of the following possible issues:

- The use of API's on mapservices.prorail.nl is changed
- The output data of the mapservices API's is changed (with added, removed or missing columns for instance)

Furthermore mapservices.prorail.nl only provides current information about the topological systems used in Dutch
Railways. As the topological systems tend to change with time, due to changing infrastructure and naming conventions, 
the current topological system is not necessarily sufficient to provide transformations on historical data. In the
future we hope to add historical topological systems as part of the functionality of this package in such a way that it
is available publicly.


## Structure

The structure of the openspoor package is largely split in two categories.

#### MapservicesData

The MapservicesData classes use mapservices.prorail.nl API's to retrieve the necessary data to perform transformations.
The essentially function as an interface with the topological systems used by ProRail.

- PUICMapservices provides general data about railway tracks (spoor) and switches (wissel and kruisingbenen). This 
contains information regarding Geocode, geocodekilometrering, but also Spoortak identificatie.
- SpoortakMapservices provides information about railway tracks concerning Spoortak identificatie and lokale 
kilometrering.

#### Transformers

The various transformers use the geopandas dataframes obtained by MapservicesData objects to add additional geographical
or topological systems to a given geopandas input dataframe. The current transformers only function for geopandas 
dataframes containing Point data. The available transformers are:

- TransformerCoordinatesToSpoor: transforms WGS84 or EPSG:28992 coordinates to spoortak and lokale kilomtrering as well 
as geocode and geocode kilometrering.
- TransformerGeocodeToCoordinates: transforms geocode and geocode kilometrering to WGS84 or EPSG:28992 coordinates.
- TransformerSpoorToCoordinates: transforms spoortak and lokale kilometrering to WGS84 or EPSG:28992 coordinates.

#### Release History

- 0.1.0
  - The first proper release
  - ADD: transform point data between geographical systems.
- 0.0.1
  - Work in progress 

#### Contributing
The openspoor package stimulates every other person the contribute to the package. To do so:

- Fork it
- Create your feature branch (git checkout -b feature/fooBar)
- Commit your changes (git commit -am 'Add some fooBar')
- Push to the branch (git push origin feature/fooBar)
- Create a new Pull Request with 3 obligated reviewers from the developement team.

You could also contribute by thinking of possible new features. The current backlog is:
- Make the package available for the "spoor" industry.