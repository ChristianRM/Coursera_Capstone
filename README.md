# IBM Data Science Capstone: Accident Severity Report

This repository contains the final project for the **IBM Data Science Professional Certificate**. The primary objective is to predict the severity of traffic accidents in Seattle using historical data to help drivers and authorities take preventive measures.

For a deep dive into the methodology and results, check out the full article on Medium:  
[**IBM Capstone Project: Accident Severity Report**](https://medium.com/@chris.ricardo.r.m/ibm-capstone-project-accident-severity-report-644224af9820)

---

## 📋 Project Overview

The project utilizes a dataset provided by the SDOT (Seattle Department of Transportation) covering collisions from 2004 to the present. A Machine Learning model was implemented to classify accident severity based on external factors such as weather, road conditions, and lighting.

### Pipeline Stages:
* **Exploratory Data Analysis (EDA):** Identified data imbalance patterns (where the majority of accidents resulted in "Property Damage Only").
* **Data Preprocessing:** Handled missing values, encoded categorical variables (One-Hot Encoding), and addressed class imbalance using **undersampling**.
* **Modeling:** Trained and evaluated multiple algorithms:
    * K-Nearest Neighbors (KNN)
    * Decision Tree
    * Support Vector Machine (SVM)
    * Logistic Regression
* **Evaluation:** Compared performance metrics using Jaccard Index, F1-score, and LogLoss.

## 🛠️ Technologies Used
* **Python** (Pandas, NumPy, Matplotlib, Seaborn)
* **Scikit-learn** (Modeling and evaluation)
* **Jupyter Notebooks**

## 📊 Key Results
The final model identifies that factors such as **rainy weather** and **wet road conditions** significantly increase the probability of severe accidents. The results suggest that an automated alert system based on these variables could effectively reduce collision rates.

## 📂 Repository Structure
* `Data_Report.ipynb`: Main notebook containing the source code for analysis and modeling.
* `Final_Report.pdf`: Detailed document covering methodology and conclusions.
* `Presentation.pdf`: Executive presentation of the project.

---

## 🧠 Personal Insights & Final Thoughts

Working with the SDOT dataset presented several real-world challenges that are worth noting:

* **Data Quality:** The raw data was notably "messy," containing numerous missing values and inconsistent labels across several features (like weather and light conditions). 
* **The Imbalance Problem:** The dataset was heavily biased toward "Property Damage Only" cases. Without applying techniques like undersampling or synthetic oversampling, any model would simply learn to predict the majority class, becoming useless for identifying high-severity risks.
* **Feature Engineering:** I found that while external conditions (weather/road) are helpful, they don't tell the whole story. Human factors—which are often harder to quantify in public datasets—likely play an even larger role in severity.
* **Conclusion:** This project highlights that Data Science is 80% data cleaning and understanding, and 20% modeling. A "perfect" algorithm cannot fix "noisy" data, but a well-preprocessed dataset can make even simple models perform exceptionally well.
