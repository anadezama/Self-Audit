# Self-Audit Documentation

Paragraph explaining process and image

Self-Audit Sources
Change a question in Audit
Form Publisher
Google Form Instructions
PowerBI 


## Self-Audit Sources

1. Google Form
   - Google Drive → Self - Audit (File responses) 
   - Google Script → DeleteOldFiles
2. Google Form Responses
3. PowerBI
4. Template
   - Google Drive → Form Publisher Output’s Folder
5. Points table 

(reports@gpmobile.net is the owner of all sources)



### 1. Google Form

This is the Self-Audit Form that gets filled out by the FOMs(1). The images that are uploaded on the Form are automatically saved in the folder called “Self-Audit(File responses)” inside the google drive (2). The images get automatically erased every monday at 1pm with the script called DeleteOldFiles (3).

(1) https://docs.google.com/a/sunholdings.net/forms/d/1m-N2uCmuza-nMP9X3PIZB8qMbnnpd9BxMiC8mz67CuU/edit?usp=forms_home&ths=true

(2) https://drive.google.com/drive/u/2/folders/0BxQ3K2juRI2NfnVOWHB6SG1FcEkyeVhlUGs5bjRfT2ZCWURDZ096ZTZUa2FnMU1zaDBWVEU

(3) https://script.google.com/u/2/home/projects/1gGI8fYGYa8lIixd66IehKsnfjRVIK-XO_GW0U16wtsqtE51i20u_XzIp

### 2. Google Forms Responses

All the google form responses get saves inside this google sheet. This google sheet is connected with PowerBI.

https://docs.google.com/spreadsheets/d/1ZQH0ohoGL4ipzDssMKqES6Sr1j1c5nLW-IQ6-oyxFdQ/edit#gid=1811552042



### 3. PowerBI


The PowerBI calculates the final grade of each Self-Audit  submitted. It also analyzes the information and gives insights. The details of the calculation process is explained below on the **PowerBI** section.



### 4. Template

This google sheet is the template that gets filled out with the Self-Audit form responses and is automatically sent to the respondent. 


https://docs.google.com/spreadsheets/d/1gQK_dDIeZ1Z_eRhKFbk8r1Si3okPYFzCQvTEWvB5kzc/edit#gid=0



### 5. Points Table

Inside this table you can find the points for every type of question in the form. This google sheet is connected with PowerBI, so if any change in points is made this google sheet needs to be modified.**

https://docs.google.com/spreadsheets/d/1-nH52f3ZHGg2MdTU5Mrznw-VtgGRG9F_kuj0dVM-4jY/edit#gid=0



## PowerBI

The PowerBI is divided into three parts: model, data and reports.
![PowerBI-Sections](https://user-images.githubusercontent.com/49915213/58035169-d3289200-7aed-11e9-9194-aafa22b85694.PNG)


### Model View/Relationship View ![Relationships Icon-PowerBI](https://user-images.githubusercontent.com/49915213/58035195-e2a7db00-7aed-11e9-94db-262d05573621.PNG) 


In the Model section we have all the connections/relationships to outside sources
![Model-PowerBI](https://user-images.githubusercontent.com/49915213/58035152-c310b280-7aed-11e9-8f7b-eef37cf68944.PNG)

##### Scores
The Scores table is connected to the google sheet where we have established the possible points of each question. If new questions are added with a different type of grading that can be added in the google sheets with the corresponding year when the changes were made. The calculators image means that it is a measure, we will explain in detail the use of the measures in the "Points Exlained" section.

Below is an example of how the scores table was built. QY means that the correct answer of the question is Yes, QN means that the correct answer is No. the 1 at the end of QY1 means the points of the question. The questions named QFR, QSKU and QV are questions that the anser is not Yes,No or N/A the answer is a value so they are graded differently

Question | Answer | Points
--- | --- | ---
QY1 | Yes | 1
QY1 | No | 0
QY1 | N/A | 0

Question | Answer | Points
--- | --- | ---
QN10 | Yes | 0
QN10 | No | 10
QN10 | N/A | 0

The questions named QFR, QSKU and QV are questions that the anser is not Yes,No or N/A the answer is a value so they are graded differently.

The options of this questions are the ones on "Answer" section and depending on the option they choose, depends on the number of points they receive. The same thing happens with QV and QFR.

Question | Answer | Points
--- | --- | ---
QSKU | 0 | 10
QSKU | 1 | 8
QSKU | 2 | 6
QSKU | 3 | 4
QSKU | 4 | 2
QSKU | 5+ | 0


##### GSresponses
In this table we can find the responses of each google form, it is connected to the Google Sheet GSResponses. If you want to add a question you have to follow the instructions in the coresponding section.

##### DimStore
This table is connected with the SQL Table named DimStore, it helps us connect the SAP store with its' corresponding FOM inside the visualizations. The administrator is Michelle Ocampo.

##### DimDate
This table is connected with the SQL Table named DimDate, it helps us give a cronological order to the visualizations in the reports section.

##### KPI
This table was created to be able to use the KPI Visualization in the reports section. We put .8 as the goal in the visualization created. The other rows are measures created so that the following visualizations don't show an error (1). This will be explained on detail in the "Visualizations" section.

(1) ![KPIs](https://user-images.githubusercontent.com/49915213/58045451-27407000-7b08-11e9-982a-d25a97015bb5.PNG)



 
 ### Report View / Visualizations  ![Report Icon - PowerBI](https://user-images.githubusercontent.com/49915213/58034650-ab84fa00-7aec-11e9-9040-39fc569f4e6b.PNG)



### Data View  ![Data - PowerBI](https://user-images.githubusercontent.com/49915213/58034999-72995500-7aed-11e9-8b4e-44a9e00e680e.PNG)



# How to calculate Points

To calculate the points we created columns and measures, here is the difference between them. DIFFERENCE
First we created calculated column for each question in the acdit naming it Category_SubCategory_Q#_Score (ex. CustomerInformation_Documentation_Q1_Score)

Num/Den








