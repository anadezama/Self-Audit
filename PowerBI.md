# PowerBI

The PowerBI is divided into three parts: model, data and reports.
![PowerBI-Sections](https://user-images.githubusercontent.com/49915213/58035169-d3289200-7aed-11e9-9194-aafa22b85694.PNG)


## Model View/Relationship View ![Relationships Icon-PowerBI](https://user-images.githubusercontent.com/49915213/58035195-e2a7db00-7aed-11e9-94db-262d05573621.PNG) 


In the Model section we have all the connections/relationships to outside sources
![Model-PowerBI](https://user-images.githubusercontent.com/49915213/58035152-c310b280-7aed-11e9-8f7b-eef37cf68944.PNG)

### Scores
The Scores table is connected to the google sheet where we have established the possible points of each question. If new questions are added with a different type of grading that can be added in the google sheets with the corresponding year when the changes were made. The calculator image means that it is a measure, we will explain in detail the use of the measures in the "Points Exlained" section.

Below is an example of how the scores table was built. QY means that the correct answer of the question is Yes, QN means that the correct answer is No. the 1 at the end of QY1 means the points of the question. 

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


### GSresponses
In this table we can find the responses of each google form, it is connected to the Google Sheet GSResponses. If you want to add a question you have to follow the instructions in the coresponding section.

### DimStore
This table is connected with the SQL Table named DimStore, it helps us connect the SAP store with its' corresponding FOM inside the visualizations. The administrator is Michelle Ocampo.

### DimDate
This table is connected with the SQL Table named DimDate, it helps us give a cronological order to the visualizations in the reports section.

### KPI
This table was created to be able to use the KPI Visualization in the reports section. We put .8 as the goal in the visualization created. The other rows are measures created so that the following visualizations don't show an error (1). This will be explained on detail in the "Visualizations" section.

(1) ![KPIs](https://user-images.githubusercontent.com/49915213/58045451-27407000-7b08-11e9-982a-d25a97015bb5.PNG)



 
 ## Report View / Visualizations  ![Report Icon - PowerBI](https://user-images.githubusercontent.com/49915213/58034650-ab84fa00-7aec-11e9-9040-39fc569f4e6b.PNG)
 
Inside this section we can find the visualizations we are using to analyze the information. 

1. 
![Visualization-ColumnGraph](https://user-images.githubusercontent.com/49915213/58100060-8652c300-7ba2-11e9-94c4-085e0e7d3ca2.PNG)![Visualization-ColumnGraph right](https://user-images.githubusercontent.com/49915213/58100184-c31eba00-7ba2-11e9-9a7e-5a32e08f8631.PNG)


The goal of this visualization is to see how many Audits each FOM has made each month. On the right side you can see we used the "Last 6 Months" column on the x-axis, this so that the graph only gets filled out by last 6 months' data and it doesn't look messy.


2.
![Visualization-FinalScore](https://user-images.githubusercontent.com/49915213/58100578-830c0700-7ba3-11e9-80f2-138a7efa707d.PNG)![Visualization-FinalScore right](https://user-images.githubusercontent.com/49915213/58100555-78517200-7ba3-11e9-95a9-81e0cc042a7a.PNG)


This visualization was made to see the grade of each Audit made by each FOM, you can see the Audits they made by SAP and month. You can also see the exact day the Audit was made. We used conditional formatting to fill out the color of the grades in red when they are below 80, in yellow if they are between .8 and .95 and green if it is .95 or above.


3.
![Visualization-Complete](https://user-images.githubusercontent.com/49915213/58100990-60c6b900-7ba4-11e9-9457-813ce805c241.PNG)![Visualization-Complete right](https://user-images.githubusercontent.com/49915213/58100992-615f4f80-7ba4-11e9-8d40-98888f53719a.PNG)


The goal of this visualization is to see if the FOM completed the form by using the calculated column "Complete/Incomplete".


4.
![Visualization-KPIs](https://user-images.githubusercontent.com/49915213/58101199-c74bd700-7ba4-11e9-92fa-9d49814e80be.PNG)![Visualization-KPIs right](https://user-images.githubusercontent.com/49915213/58101202-c9159a80-7ba4-11e9-9b36-3eedba5d0de5.PNG)


This visualization is to see the average grade by section and the average of the final score. The goal of every KPI is 80 and we used a Measure to make sure the KPI doesn't give an error, the formula is explained on the section **Calculated Columns and Measures**.


5.
![Visualization-ColumnGraphsCategory](https://user-images.githubusercontent.com/49915213/58102055-4ab9f800-7ba6-11e9-8c42-a86a9f5e3f0d.PNG)![Visualization-ColumnGraphsCategory right](https://user-images.githubusercontent.com/49915213/58102059-4c83bb80-7ba6-11e9-8f1e-d6e0ca2a5ee3.PNG)


This visualization is to see which Subcategory has the highest and lowest grade. On the Value section we can find the Measure created for each subcategory insede the Scores table.


6.
![Visualization-Table](https://user-images.githubusercontent.com/49915213/58102515-011ddd00-7ba7-11e9-988b-1fa03aad85aa.PNG)![Visualization-Table right](https://user-images.githubusercontent.com/49915213/58102521-02e7a080-7ba7-11e9-96a8-6378ac86c5e5.PNG)


This visualization was created to see the grade of each category and subcategory of every Audit responded. We can see that in "Values" section are all the Measures of each category and subcategory.


## Data View  ![Data - PowerBI](https://user-images.githubusercontent.com/49915213/58034999-72995500-7aed-11e9-8b4e-44a9e00e680e.PNG)

Inside this section you can see the columns and measures that are inside each source we previosuly mentioned.
![DataView](https://user-images.githubusercontent.com/49915213/58102809-843f3300-7ba7-11e9-887a-c1e6faf93ab2.PNG)

