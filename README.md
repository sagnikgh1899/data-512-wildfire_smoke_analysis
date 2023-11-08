[![GitHub license](https://img.shields.io/github/license/sagnikgh1899/data-512-homework_1)](https://github.com/sagnikgh1899/data-512-homework_1/blob/main/LICENSE)
# DATA 512: Human Centered Data Science (Autumn 2023)

Part 1 - Common Analysis sets the stage for the subsequent assignments. In Part 1 we will conduct a base analysis. All of the students in the class will conduct the same analysis, but with a slightly different data subset.

## Common Analysis
More and more frequently summers in the western US have been characterized by wildfires with smoke billowing across multiple western states. There are many proposed causes for this: climate change, US Forestry policy, growing awareness, just to name a few. Regardless of the cause, the impact of wildland fires is widespread. There is a growing body of work pointing to the negative impacts of smoke on health, tourism, property, and other aspects of society.
The course project will require that we analyze wildfire impacts on a specific city in the US. The end goal is to be able to inform policy makers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires.

The common research question that we are to answer is:

**What are the estimated smoke impacts on the assigned city (Tulare) for the last 60 years?**

We are to create an annual estimate of wildfire smoke in our assigned city. This estimate is just a number that we can eventually use to build a predictive model. Technically, smoke impact should probably be considered the health, tourism, economic or other social problems that result from the smoke. For this we'll generically call our estimate the wildfire smoke impact. We will consider other potential social and economic impacts during Part 2 of the course project. For now, we need some kind of number to represent an estimate of the smoke our city saw during each annual fire season.
Why is this an estimate of fire smoke? These are estimates because of a number of problems that are not easy to resolve and simplifications to make this course project reasonable for just a few weeks of work. One example is that actual smoke impact is based on wind direction over a course of several days, the intensity of the fire, and its duration. However, the fire polygon data only gives a year for each fire - it does not provide specific start and end dates for the fire. 
The smoke estimate should adhere to the following conditions:
- The estimate only considers the last 60 years of wildland fires (1963-2023).
- The estimate only considers fires that are within 1250 miles of the assigned city (Tulare).
- An annual fire season will run from May 1st through October 31st.


## Data Sources
The following is the data source:
- **USGS_Wildland_Fire_Combined_Dataset.json**: The common analysis research question is based on one specific dataset which can be found at [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81). This dataset was collected and aggregated by the US Geological Survey. The dataset is relatively well documented. Fire polygons are available in ArcGIS and GeoJSON formats. We have been assigned one US city that will form the basis for our individual analysis. We can find our individual US city assignment from [this Google spreadsheet](https://docs.google.com/spreadsheets/d/1cmTW5fgU3KyH6JbrRao-qWjzu2GovKk_BkA7a-poGFw/edit?usp=drive_link).


## Link to licensed sample notebook
The below sample codes were referenced for the following tasks and have been provided under the [Creative Commons](https://creativecommons.org/) [CC-BY license](https://creativecommons.org/licenses/by/4.0/):
- [Sample notebook for Geodetic Distance Computation](https://drive.google.com/file/d/1qNI6hji8CvDeBsnLDAhJXvaqf2gcg8UV/view?usp=sharing)
- [Sample code for accessing the US EPA Air Quality System API](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view?usp=sharing)
- [Sample code for GeoJSON reader](https://drive.google.com/file/d/1TwCkvdaw0MxJzW7NSDg6XxYQ0dvaS44I/view?usp=sharing)

## Data files

#### Library installation required
 - pyproj
 - geojson
 - tqdm
 - seaborn
 - matplotlib
 - statsmodels
 - requests

#### Repository tree
```
.
├── data/
│   └── Wildland_Fire_Polygon_Metadata.xml
├── images/
│   ├── Annual_Acres_Burned_in_Proximity_to_Tulare.png
│   ├── Fire_Distribution_by_Distance_from_Tulare.png
│   └── Fire_Smoke_Estimate_vs_AQI_in_Tulare.png
├── intermediate data/
│   ├── annual_smoke_estimate.csv
│   ├── final_aqi_each_year.csv
│   ├── gaseous_aqi_data_processed.csv
│   ├── gaseous_data.json
│   ├── particulate_aqi_data_processed.csv
│   └── particulate_data.json
├── reports/
│   ├── Visualization Descriptions and Reflection.docx
│   └── Visualization Descriptions and Reflection.pdf
├── src/
│   ├── Analysis_Prediction_And_Visualization.ipynb
│   ├── Compare_Smoke_Estimate_With_AQI.ipynb
│   ├── Data_Acquisition.ipynb
│   └── Get_AQI_Per_Year.ipynb
├── LICENSE
└── README.md
```

#### Description
- **data** : This directory contains data files, including metadata about the wildland fire polygons.
- **images** : Here, we'll find visualizations that provide insights into the annual acres burned in proximity to Tulare, the distribution of fires by distance from Tulare, and the relationship between fire smoke estimates and Air Quality Index (AQI) in Tulare.
- **intermediate data** : This directory stores intermediate data files used in the analysis, including processed data related to smoke estimates, AQI data, and more.
- **reports** : This directory contains reports in both Word and PDF formats, providing descriptions and reflections on the project's visualizations and findings.
- **src** : The source code for the project is located here. It includes Jupyter Notebook files that cover various aspects of the analysis, prediction, data acquisition, and AQI per year.
- **LICENSE** : A file that contains an MIT LICENSE for sagnikgh1899/data-512-wildfire_smoke_analysis repo.
- **README.md** : A file that contains information to reproduce the analysis, including data descriptions, attributions and provenance information, and descriptions of all relevant resources and documentation (inside and outside the repo) and hyperlinks to those resources.



## Special Considerations
- Because of the large size of the "USGS_Wildland_Fire_Combined_Dataset.json" file it could not be uploaded on GitHub. Therefore to reproduce the results it is imperative to download the GeoJSON Files.zip from [this link](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) and extract the "USGS_Wildland_Fire_Combined_Dataset.json" file and place it under the data folder.
- The "all_fire_data_with_distance.csv" file is not present under the intermediate data folder because of its large size. However, if one follows the steps mentioned below to reproduce the analysis, it will be generated and no manual intervention is required.
- Fires have been filtered based on their distance from the city (maximum 1250 miles permissible) and the fire year (1963 to 2023 only)
- Since the fire date is quite messy, all fires for an year have been considered instead of just focusing on the fires between May 1st till October 31st.
- There are 35 instances of curveRings out of the 135061 instances, so we can choose to ignore them without much impact on the overall result.


## Reproducing the analysis
To reproduce this analysis, follow these steps:
1. Clone this repository to the local machine.
2. Ensure that Python is installed with the required libraries.
3. Download the GeoJSON Files.zip from [this link](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) and extract the "USGS_Wildland_Fire_Combined_Dataset.json" file and place it under the data folder.
4. Run Data_Acquisition.ipynb to generate the dataset "all_fire_data_with_distance.csv" inside the 'intermediate data' folder that will be required for further analysis.
5. Next, run Analysis_Prediction_And_Visualization.ipynb to get the smoke estimate, build a prediction model and generate two of the visualizations.
6. Then, run Get_AQI_Per_Year.ipynb to generate the "final_aqi_each_year.csv" dataset.
7. Finally, run the Compare_Smoke_Estimate_With_AQI.ipynb file to compare smoke estimate with obtained AQI and generate the third plot.
8. Analyze the results.

*Feel free to use, modify, or contribute to this project while adhering to the MIT License.*


## Best practices for documentation
- PEP 8 – Style Guide for Python Code ([Reference link](https://peps.python.org/pep-0008/))
- Use of relative path addresses to help in reproducibility
- Use of intuitive variable and function names to ease in understanding
- Appropriate comments and documentation provided for the data aquisition, data processing and data analysis steps
- Description of all data files present in the repository mentioned

## Author
[Sagnik Ghosal](https://github.com/sagnikgh1899)