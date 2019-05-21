# Self-Audit Documentation

Paragraph explaining process and image

[Sources](/Sources.md)

[PowerBI](/PowerBI.md)

[Calculated Columns and Measures](/Calculated Columns and Measures.md)

Change a question in Audit

Form Publisher

Google Form Instructions

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


Measures created inside KPI table:

1. KPI Goal Category (4 created for each category and 1 for Final Score)

**1. KPI Goal Category**

This measures are used in the Visualization section, to fill out the KPI "Target Goal". We used this formula so the KPI doesn't give an "Error" when the category has no information to take from.

KPI  Goal Category =

IF ( ISBLANK ( [Category] ), BLANK (), .8 )











