# <center> **IBM CAPSTONE PROJECT FINAL REPORT** </center>
## <center> **Car Accident Severity** </center>

**<center>Christian Rincon</center>**
<br>
<br>

---
**<i>Abstract</i>**
<i>
    This document presents the development of a prediction model fed with a car accident registry from an open data shared by the Seattle government. The objective of the resulting model is to, based on the weather and road conditions, warn about the possibilities of being involved in a car accident and how severe it could be.
</i>

### Business Understanding:
The government of Seattle has a registry of automobile accidents[1] that have occurred since 2004, and is interested in obtaining insights or applying some type of measure to inform its drivers of the dangers that exist when driving. According to WHO[2] (World Healt Organization) the yearly fatalities caused by a road traffic crash is around 1.35 million, and almost 3,700 every day. This projects main focus is to analize the data, for any relevant information that may help then understanding of the topic and the creation of a model that can predict the risk and level of severity of an accident.
<!-- The initial phase is to understand the project's objective from the business or application perspective. Then, you need to translate this knowledge into a machine learning problem with a preliminary plan to achieve the objectives. -->

### Data understanding:
The data used in this report includes all types of collisions. Collisions were provided by SPD and recorded by Traffic Records. The dataset contains 221,525 rows and 40 columns, this is the raw data and may differ later on due to data cleaning.
The dependent variable in this set is named "SEVERITYCODE",and its value refers to the possible outcomes:
<br>• 3—fatality <br>• 2b—serious injury <br>• 2—injury <br>• 1—prop damage <br>• 0—unknown 

The data set is summarized as shown in the following table (Extracted from the attribute information document[3]):

| Attribute           | Data type, length | Description                                                                                                                                        |
|---------------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| OBJECTID            | ObjectID          | ESRI unique identifier                                                                                                                             |
| SHAPE               | Geometry          | ESRI geometry field                                                                                                                                |
| INCKEY              | Long              | A unique key for the incident                                                                                                                      |
| COLDETKEY           | Long              | Secondary key for the incident                                                                                                                     |
| ADDRTYPE            | Text, 12          | Collision address type:     <br>•Alley <br>•Block <br>• Intersection                                                                                                                       |
| INTKEY              | Double            | Key that corresponds to the intersection associated with a collision                                                                               |
| LOCATION            | Text, 255         | Description of the general location of the collision                                                                                               |
| EXCEPTRSNCODE       | Text, 10          |                                                                                                                                                    |
| EXCEPTRSNDESC       | Text, 300         |                                                                                                                                                    |
| SEVERITYCODE        | Text, 100         | A code that corresponds to the severity of the collision:    <br>• 3—fatality <br>• 2b—serious injury <br>• 2—injury <br>• 1—prop damage <br>• 0—unknown                                                                                     |
| SEVERITYDESC        | Text              | A detailed description of the severity of the collision                                                                                            |
| COLLISIONTYPE       | Text, 300         | Collision type                                                                                                                                     |
| PERSONCOUNT         | Double            | The total number of people involved in the collision                                                                                               |
| PEDCOUNT            | Double            | The number of pedestrians involved in the collision. This is entered by the state.                                                                 |
| PEDCYLCOUNT         | Double            | The number of bicycles involved in the collision. This is entered by the state.                                                                    |
| VEHCOUNT            | Double            | The number of vehicles involved in the collision. This is entered by the state.                                                                    |
| INJURIES            | Double            | The number of total injuries in the collision. This is entered by the state.                                                                       |
| SERIOUSINJURIES     | Double            | The number of serious injuries in the collision. This is entered by the state.                                                                     |
| FATALITIES          | Double            | The number of fatalities in the collision. This is entered by the state.                                                                           |
| INCDATE             | Date              | The date of the incident.                                                                                                                          |
| INCDTTM             | Text, 30          | The date and time of the incident.                                                                                                                 |
| JUNCTIONTYPE        | Text, 300         | Category of junction at which collision took place                                                                                                 |
| SDOT_COLCODE        | Text, 10          | A code given to the collision by SDOT.                                                                                                             |
| SDOT_COLDESC        | Text, 300         | A description of the collision corresponding to the collision code.                                                                                |
| INATTENTIONIND      | Text, 1           | Whether or not collision was due to inattention. (Y/N)                                                                                             |
| UNDERINFL           | Text, 10          | Whether or not a driver involved was under the influence of drugs or alcohol.                                                                      |
| WEATHER             | Text, 300         | A description of the weather conditions during the time of the collision.                                                                          |
| ROADCOND            | Text, 300         | The condition of the road during the collision.                                                                                                    |
| LIGHTCOND           | Text, 300         | The light conditions during the collision.                                                                                                         |
| PEDROWNOTGRNT       | Text, 1           | Whether or not the pedestrian right of way was not granted. (Y/N)                                                                                  |
| SDOTCOLNUM          | Text, 10          | A number given to the collision by SDOT.                                                                                                           |
| SPEEDING            | Text, 1           | Whether or not speeding was a factor in the collision. (Y/N)                                                                                       |
| ST_COLCODE          | Text, 10          | A code provided by the state that describes the collision. For more information about these codes, please see the State Collision Code Dictionary. |
| ST_COLDESC          | Text, 300         | A description that corresponds to the state’s coding designation.                                                                                  |
| SEGLANEKEY          | Long              | A key for the lane segment in which the collision occurred.                                                                                        |
| CROSSWALKKEY        | Long              | A key for the crosswalk at which the collision occurred.                                                                                           |
| HITPARKEDCAR        | Text, 1           | Whether or not the collision involved hitting a parked car. (Y/N)                                                                                  |

<!-- In this phase, you need to collect or extract the dataset from various sources such as csv file or SQL database. Then, you need to determine the attributes (columns) that you will use to train your machine learning model. Also, you will assess the condition of chosen attributes by looking for trends, certain patterns, skewed information, correlations, and so on. -->

### Data Preparation:
Here is presented the construction of the final dataset in order to be fed to the algorithms.
The previously shown data set had a lot of extra columns and null vaues, also the column 'INCDATE' will be useful in the creation of new columns that may help having an understanding of the data.

Using the column 'INCDATE' the values were parsed and split in order to show the reader the number of accidents by year, month, and day of week.

The year with the highest number of registered incidents was 2005

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/incidents_per_year.JPG?raw=true" width="550">

The month with the highest number of registered incidents was October

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/%C3%ACncidents_by_month.JPG?raw=true" width="550">

The day of the week with the highest number of registered incidents was Friday

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/incidents_by_dayofweek.JPG?raw=true" width="550">



As of the severity code the values were also plotted and the results are as follows, being the code '1' the most registered (this code being property damage).

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/severitycode_distribution.JPG?raw=true" width="550">


Lastly in this data preparation, the null values were dropped then categorical was asigned value.

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/other_data_distribution.JPG?raw=true" width="550">


<!-- The data preparation includes all the required activities to construct the final dataset which will be fed into the modeling tools. Data preparation can be performed multiple times and it includes balancing the labeled data, transformation, filling missing data, and cleaning the dataset. -->

### Modeling:
In this phase, three algorithms different models were trained, these for each of these algorithms:
* KNN (K Nearest Neighbor)
* Decision Tree
* Support Vector Machine (SVM)

The data set was split into: 
80% training set
20% testing set

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/set_split.JPG?raw=true" width="550">


### Building of the models:
The three models are built using the same test and train set.
<b>KNN</b>
First, the best k is selected via iterative testing

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/best_k%20(2).jpg?raw=true" width="550">

Then the model is built

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/knn_model.JPG?raw=true" width="550">

<b>Decision Tree</b>
The decision tree model was built as shown next

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/dt_model.JPG?raw=true" width="550">

<b>SVM</b>
The support vector machine was defined this way

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/svm_model.JPG?raw=true" width="350">



### Comparison of the models:
Once the models were evaluated, the results were as shown in the next image, being the SVM model the one with the best score.

<img src="https://github.com/ChristianRM/Coursera_Capstone/blob/master/img/comparison.JPG?raw=true" width="300">

<!-- In this phase, various algorithms and methods can be selected and applied to build the model including supervised machine learning techniques. You can select SVM, XGBoost, decision tree, or any other techniques. You can select a single or multiple machine learning models for the same data mining problem. At this phase, stepping back to the data preparation phase is often required. -->
### Conclusion:
Based on the obtained results in this project it is concluded that some conditions may infer in the result. Also due to the target value being non-binary the models were not able to predict with a greater presicion.

<!-- The deployment phase requirements vary from project to project. It can be as simple as creating a report, developing interactive visualization, or making the machine learning model available in the production environment. In this environment, the customers or end-users can utilize the model in different ways such as API, website, or so on. -->

### Acknoledgements
1 Collisions. Seattle GeoData. 
https://data-seattlecitygis.opendata.arcgis.com/datasets/5b5c745e0f1f48e7a53acec63a0022ab_0
Last Accesed 9/19/2021

2 GLOBAL STATUS REPORT ON ROAD SAFETY 2018. World Health Organization. https://www.who.int/publications/i/item/global-status-report-on-road-safety-2018 ISBN: 9789241565684

3 Collisions Data Set Summary. Seattle GeoData. 
https://www.seattle.gov/Documents/Departments/SDOT/GIS/Collisions_OD.pdf
Last Accesed 9/19/2021