# Bodies: Foreign and Celestial 
 
## Code Louisville Data Analysis Course 2 Fall 2022
 
As a health inspector, I am tasked with responding to the concerns and questionable choices of the public. On particularly strange days, my office often asks, “Why are people being so weird, is it a full moon tonight?” While the so-called [lunar effect](https://en.wikipedia.org/wiki/Lunar_effect) of people acting particularly strange on full moon days is a widely accepted truth to many people in public service, actual research on it is not quite as conclusive. The purpose of this project is twofold: 
Are there more visits to the Emergency Department for foreign objects in patients during full moons?
General exploration of the NEISS data. Who is going to the Emergency Department for having foreign objects in their bodies? Which body parts are the most commonly injured and which objects are people getting stuck in their bodies? Are there any clear differences between visits involving adults and children? 
 
 
## Data Dictionaries


| Field        | Definition           | Description of Codes  |
| ------------- |:-------------:| -----:|
| Disposition      | patient status upon/after ED Visit | 1-9 |
|      |       |  1 - Treated/Examined and Released |
|      |     |    2 - Treated and Transferred |
|      |     |   4 - Treated and Admitted/Hospitalized |
|      |     |   5 - Held for Observation |
|      |     |    6 - Left Without Being Seen |
|      |     |    8 - Fatality, Incl. DOA, Died in ER |
|      |     |    9 - Unknown, Not Stated |
|      |     |    2 - Treated and Transferred |
|      |     |    2 - Treated and Transferred |


| Field        | Definition           | Description of Codes  |
| ------------- |:-------------:| -----:|
| Location      | location where incident occurred | 0-9 |
|      |     |    0 - Not Recorded |
|      |       |  1 - Home |
|      |     |    2 - Farm/Ranch |
|      |     |   4 - Street/Highway |
|      |     |   5 - Other Public Property |
|      |     |    6 - Mobile/Manufactured Home |
|      |     |    7 - Industrial |
|      |     |    8 - School/Daycare |
|      |     |    9 - Place of Recreation or Sports |

 
 
This project primarily uses data queried from the National Electronic Injury Surveillance System (NEISS). The Consumer Product Safety Commission collects Emergency Department surveillance data from approximately 100 participating hospitals on consumer product-related injuries occurring in the United States. For this project, the NEISS Query Builder was used to gather all cases from 2017-2021 for diagnosis codes for aspirated objects, ingested objects, and foreign bodies for all ages and body parts. This data was grouped by year and saved as a csv. It was combined with a separate CSV which contains product codes and titles. The combined dataframe was altered by dropping columns not relevant to the project and entries for irrelevant diagnosis codes. Some exploration of the data was done to see if any trends could be found with regard to gender, drug use, alcohol involvement, fire involvement, location where the incident occured, and patient status after being seen in the hospital. 
 
A dictionary of body part names and codes was created and combined with the existing dataframe to more easily understand the data. The cleaned up and combined NEISS data was saved for use in a Tableau dashboard. This dashboard displays additional visualizations about the age breakdown of patients and the products and body parts most commonly involved in ED visits for all patients, and for children and adults. A custom color palette modeled after the Viridis palette was used to increase accessibility for individuals who may have red-green colorblindness. 
 
A second dataframe was created using data pulled from Visual Crossing Weather. This data included information about moon phases for each day of 2017-2021. For ease of reading, a column was added to this dataframe with text for each moon phase. A second column was added with more broad lunar phase categories. An additional column was added to show a corresponding moon emoji for each phase to provide an easy to understand visual representation of each moon phase. 
 
A count of visits for each treatment day was calculated using the original merged dataframe. The Bokeh library was used to plot out daily Emergency Department visits and moon phase on a dual y axis linegraph. This graph was used to visually see any potential spikes in treatment days and full moons over time.
 
The moon phase dataframe and NEISS dataframe were joined on the date and irrelevant columns were dropped. From this information, a new dataframe with the count of days and emergency department visits of each lunar phase was created by aggregating by the moon phase. This simplified dataframe was used to create a nested pie chart showing the percentage of days and emergency department visits in each moon phase. This chart serves as a visual representation to determine if a relatively large percentage of emergency department visits occurred in any particular moon phase. It does not appear to be the case. These results seem to suggest we cannot, in fact, blame the full moon for this specific sort of strange behavior. An alternate hypothesis of, “that’s just how people are” cannot be rejected at this time.  
 
The original NEISS data was later grouped by some of the most commonly impacted body parts. Narratives from these encounters were combined, stop words were removed, and word clouds for each body part were created. A final word cloud using all narratives in the dataframe was also created.
 
Cleaned up NEISS data was saved as a csv and used to create a Tableau dashboard. This dashboard includes a racing bar chart comparing the ranks of most commonly injured body parts over time, a tree map of the products most often involved in ED visits, a bar chart of visits grouped by patient age, and a Word Cloud made from the patient encounter narratives. The dashboard includes navigation buttons to switch between data for only children, only adults, and all patients. It is best viewed in full screen mode on desktop. [The Tableau dashboard can be found here.](https://public.tableau.com/views/VeryNEISS/ChildDash?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)
 
 
## Setup

### pip setup 
Clone this repository.
 
Create a virtual environment
python -m venv neiss-env

Activate your environment

Windows:
 . neiss-env/Scripts/activate

Mac/Linux:
source neiss-env/bin/activate 

#### Requirements
This project uses Python 3.9.7

Before starting, install the project's dependencies with
```pip install -r requirements.txt```
 
### conda setup
If pip setup is unsuccessful due to a missing wordcloud wheel file for your operating system/python version, you can try to install wordcloud with [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html) and the remainder with pip by entering these commands into your terminal:
 
Steps to create a conda environment named neiss-env are listed below.
 
Step 1: Create a conda environment.
 
conda create -n neiss-env jupyter notebook
 
Step 2: Activate the environment using the command
conda activate neiss-env
 
Step 3: Install the packages
```conda install -c conda-forge wordcloud
pip install emoji bokeh pandas-bokeh datetime notebook numpy pandas seaborn matplotlib wordcloud 
```
 
Step 4: After activating the neiss-env, check the packages that are installed using the command
conda list 
 
 
Additional information about managing environments can be found here
 
https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html
 
 
### Environment
This project utilizes Jupyter Notebook and can be run in a Jupyter Notebook or displayed using the Jupyter Notebook add on to VS Code. 
 
##  Run Notebook
From the command line, launch Jupyter Notebook 
```jupyter notebook```

open `very_neiss.ipynb`

### Data Sources
Visual Crossing Corporation. Visual Crossing Weather. 2017-2021, https://www.visualcrossing.com/. Accessed June 26, 2022.
 
Consumer Product Safety Commission. National Electronic Injury Surveillance System 2002-2021 on NEISS Online Database, released April, 2022. Generated at https://www.cpsc.gov/cgibin/NEISSQuery/home.aspx. on: June 17, 2022 at 16:39:24
 
The 2017-2021MoonPhase.csv, AllNEISS.csv, and product_codes.csv are all publicly saved on a Google Drive and will be downloaded automatically by Pandas.
 
## Code Louisville Project Features:
 
### Category 1: Loading data.
 - Read TWO data files 
 
### Category 2: Clean and operate on the data while combining them.
 - Clean data and perform pandas merge with datasets and perform calculations on the new dataset.
 - Join text data found in narratives and display the most commonly used words. 
 
### Category 3: Visualize /Present data.
 - Make a Tableau dashboard to display data
 - Make visualizations with Bokeh
 - Most frequently used words from narratives displayed in word clouds.
 
### Category 4 Best Practices:
 - Utilize a virtual environment and include setup instructions in README.
 - Build a custom data dictionary and include it in README.
 - List dependencies in a requirements.txt file 
 
### Additional features:
 - Use a Jupyter notebook to document your data analysis.
 - A custom color scheme based on the Viridis color palette was used throughout to increase accessibility for individuals with red-green colorblindness. 
 

