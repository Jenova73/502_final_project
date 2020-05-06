




# Coco Final Report 
Massive Data Fundamentals - Spring 2020


Group Menbers:
Zhenkun Wang
Yuzheng Xie
Yunxi Zhang
Rujin Guo










# Introduction 

Data Science Question: 
Background (NYC, 311)
Reason:

New York City is located in New York State in the northeastern United States. It is the most populous city in the United States and one of the largest cities in the world. As the most densely populated major city in the United States, New York ranks first among the nation's metropolises with a population of 19.8 million. It has the most diverse language and population group in the United States, where 800 languages are spoken. The dense population, the changing social structure, and the emergence of multiple languages, cultures, and customs have brought about various social disputes and needs for help.

The 311 service request group first launched in 2003, and its data set started in 2004 and is updated daily. It contains about 20G of data. New Yorkers can connect to 311 online via text, phone or social media. The NYC311 call center provides 180 languages and more than 50 languages online to suit and better serve diverse ethnic groups.

Take a brief look at the dataset we have got for 2018:

In 2018, 44,023,630 customers requested services or information, which is 10.2% higher than the highest record in 2017. With the popularity of the Internet, the digital address book surpassed the traditional telephone channel for the first time in the history of 311 years. Although 20.9 million customers dialed 311 through the telephone channel, the interaction through digital channels such as websites, apps, and social media has grown rapidly, reaching 16.6%.

NYC311 can provide a wide range of services, including homeless assistance, pothole repairs, or help understanding property tax bills. The number of service requests has greatly increased, and noise complaints, illegal parking and lane blockages are still major issues. The public will be most concerned about how long it will take the service center to complete the request? People need to understand the efficiency of 311.

The project will analyze the accuracy of the eTo this end, New York City has set up 311 service requests as the main source of New York City government information and non-emergency services to provide the public with fast and convenient New York City government services and information. 

stablished model, which focuses on predicting the number of days to complete the request.


# Dataset Introduction and cleaning

This dataset is collected from NYX 311 Service Requests for 2004. This dataset has 52 columns. First, all N/A values have been dropped. In this analysis, 14 columns were kept and used, including “Created Date”, “Closed Date”, “Agency”, “Agency Name”, “ Complaint Type”, “ Descriptor”, “ Location Type”, “Incident Zip”, “City”, “ Status”, “ Community Board”, “Borough”, “Park Borough”, “Latitude” and “Longitude”. “Agency Name” refers to the name of the responding city government agency. “Complaint Type” refers to the topic of the incident or condition. 

Created Date” and “Closed Date” are in the string format like  “YYYY/MM/DD”. After changing them to date format by “to_date”, three new columns are created: Year(created), month(created) and Time. In order to predict how many days a request can be completed based on different features, “Time” is created by calculating the time gap between the “Created Date” and “Closed Date”.  Then a new column with Timebin replaced the Time as the label of model for better prediction. As Timebin, label has been divided into three columns: within 2 days, within a week and more than a week.

Analysis and modeling
To assist having a better understanding of the dataset, some basic exploratory data analysis was conducted based on the pyspark.sql package and the Matplotlib.pyplot package. Firstly, the top five frequent complaint types are listed, which are heating, noise-residential,  heat/hot water, plumbing, and blocked the driveway. A bar chart was made as follows.

Figure-top five frequent complaint types
Then, top five frequent agencies are shown in the plot below. 

Figure- top five frequent agencies














 The top five frequent cities are shown in the plot below. 




The project is based on the Spark Pipeline which contains transformers and estimators. After cleaning data including merging datasets, dropping useless columns, creating a new column and etc., the first step is string indexing. ‘StringIndexer( )’ and other indexers are used to assign unique integers value to each category data. Then, the‘VectorAssembler’ is used to specify the input and output columns in order to train the machine learning models. After that, machine learning models were built. The next step is to fit the pipeline for the trained data and predict for the test data.
 
There are two machine learning models used in this project. The first one is the Logistic Regression model. The label column is ‘Timebin’, which indicates the time used to process the case. The label has three categories---Low, Medium, High. The features include ‘Agency’, ‘Complaint Type’, ‘Location Type’, ‘City’, ‘Borough’ and etc. The second model is Random Forest. For this model, the label and features of the data are the same as the Logistic Regression model. 


# Results
According to the results, for the Logistic Regression model, there are three criteria to evaluate the model performance----F1-Score (0.54), Precision (0.52), Recall (0.60), Accuracy (0.60).

To make the result more readable, a confusion matrix was made as follows.
 
Figure- confusion matrix for Logistic Regression
The results for the Random Forest model are as follow.

To make the result more readable, a confusion matrix was made as follows.

Figure- confusion matrix for Random Forest
Based on the results, the Random Forest Model performs better than the Logistic Regression model with a higher accuracy 0.71.

It is easy to see that most cases can be finished within a week. Even the random forest model believes no case will take more than a week. It means agencies in new york are quite high efficient, only particular cases would take a long time.
 

Division of labor:
Yunxi Zhang and Rujin Guo: Data collection and cleaning and basic analysis on dataset
Zhenkun Wang and Yuzheng Xie: EDA and model building 


# References:
https://data.cityofnewyork.us/Social-Services/311-Service-Requests-for-2007/aiww-p3af

https://www1.nyc.gov/311/nyc311-enhances-service-request-open-dataset.page

https://www1.nyc.gov/311/311-sets-new-record-in-2018.page

https://www.ny.gov/agencies/nyc-311

https://scikit-learn.org/0.18/auto_examples/model_selection/plot_confusion_matrix.html

