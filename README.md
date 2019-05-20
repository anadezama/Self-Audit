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



# Calculated Columns & Measures (How to calculate Points)

Num/Den

To calculate the points we created columns and measures, here is the difference between them. DIFFERENCE


## Calculated Columns:

All calculated columns were created inside the GSResponses

1. Category_Denom (For each one of the 4 categories)
2. Category_Subcategory_Denom (For each subcategory)
3. Category_Subcategory_Q#_Score (For each question inside each category)
4. Category_Blanks
5. Complete/Incomplete
6. 6 months

Formula explanation of each column:

**1. Category_Denom**

Category_Denom =
GSResponses[Category_Subcategory1_Denom] + GSResponses[Category_Subcategory2_Denom]

(You need to add all the existent categories inside the category)

Example:

CustomerInformation_Denom = 
GSResponses[CustomerInformation_Documentation_Denom] + GSResponses[CustomerInformation_EC_Denom]

**2. Category_Subcategory_Denom**

In this formula you ask if the answer of the Question is N/A or it is blank then the points are 0, or else you put the according points from the column Questions in table Points. It takes the points from the table depending on the QY or QN you insert.

Category_Subcategory_Denom=


// Denominator for Q#

    IF(GSResponses[Category_Subcategory_Q#] = "N/A" || ISBLANK(GSResponses[Category_Subcategory_Q#]),
        0, 
        CALCULATE(MAX(Scores[Points]),FILTER(Scores, Scores[Question] =  "QY/N#"))
    ) 
    
(You add the formula for the number of questions in the subcategory)

Example:

CustomerInformation_Documentation_Denom = 


// Denominator for Q1

    IF(GSResponses[CustomerInformation_Documentation_Q1] = "N/A" || ISBLANK(GSResponses[CustomerInformation_Documentation_Q1]),
        0, 
        CALCULATE(MAX(Scores[Points]),FILTER(Scores, Scores[Question] =  "QN10"))
    ) +
      
// Denominator for Q2

    IF(GSResponses[CustomerInformation_Documentation_Q2] = "N/A" || ISBLANK(GSResponses[CustomerInformation_Documentation_Q2]),
        0, 
        CALCULATE(MAX(Scores[Points]),FILTER(Scores, Scores[Question] =  "QN10"))
    )

**3. Category_Subcategory_Q#_Score**

This column basically looks for the response the FOM wrote on the form and depending on the answer they wrote down it goes to the "Points" table and gives the corresponding points. This calculation is made for each question in the Audit.

Category_Subcategory_Q#_Score =

lookupvalue(Scores[Points],Scores[Answer],GSResponses[Category_Subcategory_Q#],Scores[Question],"QY/N#")


Example:

CustomerInformation_Documentation_Q1_Scores =

lookupvalue(Scores[Points],Scores[Answer],GSResponses[CustomerInformation_Documentation_Q1],Scores[Question],"QN10")


**4. Category_Blanks**

This column calculates the number of blank questions by category. There are four calculated columns with this formula since there are four categories.

Categoty_Blanks=

VAR DQ# = IF(ISBLANK(GSResponses[Category_SubCategory_Q#),1,0)

RETURN

DQ#

Example:

CustomerInformation_Blanks = 

//Documentation

VAR   DQ1 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q1]),1,0) 
VAR   DQ2 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q2]),1,0) 
VAR   DQ3 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q3]),1,0) 
VAR   DQ4 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q4]),1,0) 
VAR   DQ5 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q5]),1,0) 
VAR   DQ6 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q6]),1,0) 
VAR   DQ7 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q7]),1,0) 
VAR   DQ8 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q8]),1,0) 
VAR   DQ9 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q9]),1,0) 
VAR   DQ10 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q10]),1,0) 
VAR   DQ11 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q11]),1,0) 
VAR   DQ12 = IF(ISBLANK(GSResponses[CustomerInformation_Documentation_Q12]),1,0) 

//Equipment Control

VAR   EQ1 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q1]),1,0) 
VAR   EQ2 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q2]),1,0) 
VAR   EQ3 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q3]),1,0) 
VAR   EQ4 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q4]),1,0) 
VAR   EQ5 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q5]),1,0) 
VAR   EQ6 = IF(ISBLANK(GSResponses[CustomerInformation_EC_Q6]),1,0) 

RETURN

DQ1+DQ2+DQ3+DQ4+DQ5+DQ6+DQ7+DQ8+DQ9+DQ10+DQ11+DQ12+EQ1+EQ2+EQ3+EQ4+EQ5+EQ6


**5. Complete/Incomplete**

This formula is to calculate if the form was completed or not.

Complete/Incomplete = 

if(
    and(
        //denominadores mayores al limite de N/As
        and(GSResponses[CustomerInformation_Denom]>=115,(and(GSResponses[CustomerFO_Denom]>=149,(and(GSResponses[InventoryM_Denom]>=72,GSResponses[StorePM_Denom]>=165))))),
        //si existen blanks en categorias
        (and(GSResponses[CustomerInformation_Blanks]=0,and(GSResponses[CustomerFO_Blanks]=0,(and(GSResponses[InventoryM_Blanks]=0,GSResponses[StorePM_Blanks]=0)))))),"Complete","Incomplete")


**6. 6 months**

This column is used in the visualizations, it is to display the information only from the last 6 months so that it looks cleaner.

Last 6 Months = 

IF (
    MAX ( GSResponses[Date] )
        > DATE ( YEAR ( TODAY () ), MONTH ( TODAY () ) - 6, DAY ( TODAY () ) ),
    "Yes",
    "No"
)


## Measures Created:

Measures created inside Scores table:
1. Category
2. Category_Num
3. Category_Den
4. Category_Subcategory
5. Final Score
6. Final_Num
7. Final_Den

Explanation of each measure

**1. Category**
This measure calculates the grade by category, dividing the Numerator created over the Denominator.

Category = 

[Category_Num]/[Category_Den]

Example:

CustomerFO =

[CustomerFO_Num]/[CustomerFO_Den]


**2. Category_Num**

This formula calculates the Numerator of a specific category. We add the Calculated Column (which basically are the points the FOM gets by his responses) of question in a specific category and that is the Numerator.

Category_Num = 

VAR

NumeratorSubcategory#1 = 

(
SUM(GSResponses[Category_SubCategory_Q#_Score]) 
)

VAR

NumeratorSubcategory#2 = 
(
SUM(GSResponses[Category_SubCategory_Q#_Score]) 
)

RETURN

    NumeratorSubCategory#1 + NumeratorSubCategory#2 


Example:

CustomerInformation_Num = 

// The variables below will calculate Numerator of Customer Information
VAR

NumeratorDoc = 
(
SUM(GSResponses[CustomerInformation_Documentation_Q1_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q2_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q3_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q4_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q5_Scores])
+SUM(GSResponses[CustomerInformation_Documentation_Q6_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q7_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q8_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q9_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q10_Scores])
+SUM(GSResponses[CustomerInformation_Documentation_Q11_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q12_Scores]) 
)

VAR

NumeratorEC = 
    SUM(GSResponses[CustomerInformation_EC_Q1_Scores]) + 
    SUM(GSResponses[CustomerInformation_EC_Q2_Scores]) + 
    SUM(GSResponses[CustomerInformation_EC_Q3_Scores]) + 
    SUM(GSResponses[CustomerInformation_EC_Q4_Scores]) +
    SUM(GSResponses[CustomerInformation_EC_Q5_Scores]) +
    SUM(GSResponses[CustomerInformation_EC_Q6_Scores])


RETURN

    NumeratorDoc + NumeratorEC 


**3. Category_Den**

This measure calculates the Denominator of the specific category. It adds the denominator of each question (Category_SubCategory_Denom) inside the category.

Category_Den = 

VAR

DenominatorSubcategory#1 = SUM(GSResponses[Category_SubCategory#1_Denom])


VAR

DenominatorSubcategory#2 = SUM(GSResponses[Category_SubCategory#2_Denom])


RETURN

    DenominatorSubcategory#1 + DenominatorSubcategory#2


Example:

CustomerInformation_Den = 

VAR

DenominatorDoc = SUM(GSResponses[CustomerInformation_Documentation_Denom])


VAR

DenominatorEC = SUM(GSResponses[CustomerInformation_EC_Denom])


RETURN

    DenominatorDoc + DenominatorEC


**4. Category_Subcategory**

This measure calculates the grade of a specific subcategory. It divides the Numerator over the denominator.

Category_SubCategory = 

VAR  

Numerator = 

(
SUM(GSResponses[Category_Subcategory_Q#_Scores]) 
)
VAR

Denominator = SUM(GSResponses[Category_SubCategory_Denom])


RETURN
    Numerator / Denominator


Example:

CustomerInformation_Documentation = 

VAR  

Numerator = 

(
SUM(GSResponses[CustomerInformation_Documentation_Q1_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q2_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q3_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q4_Scores])  
+SUM(GSResponses[CustomerInformation_Documentation_Q5_Scores])
+SUM(GSResponses[CustomerInformation_Documentation_Q6_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q7_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q8_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q9_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q10_Scores])
+SUM(GSResponses[CustomerInformation_Documentation_Q11_Scores]) 
+SUM(GSResponses[CustomerInformation_Documentation_Q12_Scores]) 
)
VAR

Denominator = SUM(GSResponses[CustomerInformation_Documentation_Denom])


RETURN

    Numerator / Denominator
    
    

**5. Final Score**

This formula calculates the final score of each audit generated.

Final Score = [Final_Num]/[Final_Den]


**6. Final_Num**

This formula calculates the numerator for the final formula. It adds the Numerator of each one of the four sections.

Final_Num = ([CustomerInformation_Num]+[CustomerFO_Num]+[InventoryM_Num]+[StorePM_Num])


**7. Final_Den**

This formula calculates the Denominator for the final formula. It adds the Denominator of each one of the four sections.

Final_Den = ([CustomerFO_Den]+[CustomerInformation_Den]+[InventoryM_Den]+[StorePM_Den])







