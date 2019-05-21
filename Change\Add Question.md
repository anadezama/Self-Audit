# Change\Add Question

To change a questions you must follow these steps:
  1. Modify the question in the [GP Mobile Self-Audit Template](https://docs.google.com/spreadsheets/d/1gQK_dDIeZ1Z_eRhKFbk8r1Si3okPYFzCQvTEWvB5kzc/edit#gid=0)
  2. Modify the question in the [Self-Audit Google Form](https://docs.google.com/forms/d/1m-N2uCmuza-nMP9X3PIZB8qMbnnpd9BxMiC8mz67CuU/edit)
  3. 

To add a questions you must follow these steps:
  1. Add the question in the [Self-Audit Google Form](https://docs.google.com/forms/d/1m-N2uCmuza-nMP9X3PIZB8qMbnnpd9BxMiC8mz67CuU/edit), also add a comment and image option with a new number of question.
  2. Modify the [GP Mobile Self-Audit Template](https://docs.google.com/spreadsheets/d/1gQK_dDIeZ1Z_eRhKFbk8r1Si3okPYFzCQvTEWvB5kzc/edit#gid=0), give the question the same format the other questions have as the image below.

![Examplequestion](https://user-images.githubusercontent.com/49915213/58108420-6e367000-7bb1-11e9-8702-a270a6b0cd62.PNG)

  3. PowerBI - Modify the name of the question to Category_SubCategory_Q# as the example below. 
  
![QuestionName1](https://user-images.githubusercontent.com/49915213/58109027-75aa4900-7bb2-11e9-8add-beb483d6417d.PNG) --> ![QuestionName2](https://user-images.githubusercontent.com/49915213/58109028-75aa4900-7bb2-11e9-8a85-e6739563944b.PNG)

  4. PowerBI - Create a column with the following formula
  
 CustomerInformation_Documentation_Q12_Scores =
  
 lookupvalue(Scores[Points],Scores[Answer],GSResponses[Category_SubCategory_Q#],Scores[Question],"QY/N#")
  
  Example:
  
 CustomerInformation_Documentation_Q12_Scores = 
  
 lookupvalue(Scores[Points],Scores[Answer],GSResponses[CustomerInformation_Documentation_Q12],Scores[Question],"QY10")

  
  5. PowerBI - Add the following formula to the corresponding Calculated column called Category_SubCategory_Denom
  
  
  
  6. PowerBI - Add the following formula to the corresponding Measure called Category_SubCategory
  
  
  
  7. PowerBI - Add the following formula to the corresponding Measure called Category_Num
  
  
  
  
  
  
