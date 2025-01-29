# LendingClub Case Study
> **Brief description of the project :**<br>
LendingClub is a financial services company headquartered in San Francisco, California.The goal of this project is to conduct an exploratory data analysis (EDA) and visualize trends, patterns, and insights in the LendingClub's loan dataset. This will help the client better understand loan distributions and identify potential defaulters in the future based on the currently available data so that it can take necessary reformations in its operations to minimize credit loss.

## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)

<!-- You can include any other section that is pertinent to your problem -->

## General Information
The goal of this project is to conduct an exploratory data analysis (EDA) and visualize trends, patterns, and insights in the LendingClub's loan dataset. This will help the client better understand loan distributions and identify potential defaulters in the future based on the currently available data so that it can take necessary reformations in its operations to minimize credit loss.
- **What is the background of this project?**<br>
LendingClub is a financial services company headquartered in San Francisco, California. It enabled borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period was three years. Investors were able to search and browse the loan listings on LendingClub website and select loans thamount of loan, lending (to risky applicants) at a higher interest rate, etc.
- **What is the dataset that is being used?**<br>
The dataset consists of information about loans issued by LendingClub. It includes borrower profiles, loan details, repayment statuses, and financial metrics. 
The key attributes of this dataset are:
1. **Loan Details:**<br>
   1.1. **Loan Amount (`loan_amnt`)**: The total loan amount requested by the borrower.<br>
   1.2. **Interest Rate (`int_rate`)**: The rate of interest charged on the loan.<br>
   1.3. **Loan Term (`term`)**: The duration of the loan (e.g., 36 or 60 months).<br>

2. **Borrower Details:**<br>
   2.1. **Annual Income (`annual_inc`)**: The borrower's yearly income.<br>
   2.2. **Employment Length (`emp_length`)**: The number of years the borrower has been employed.<br>
   2.3. **Home Ownership (`home_ownership`)**: The borrower's homeownership status (e.g., RENT, OWN, MORTGAGE).<br>

3. **Loan Purpose:**<br>
   3.1. **Purpose (`purpose`)**: The reason for taking the loan (e.g., debt consolidation, credit card payments, home improvement).<br>

4. **Loan Status:**<br>
   4.1. **Loan Status (`loan_status`)**: Indicates whether the loan is fully paid, charged off, or current.<br>

5. **Credit History:**<br>
   5.1. **FICO Score (`fico_range`)**: The borrower's credit score range.<br>
   5.2. **Debt-to-Income Ratio (`dti`)**: A measure of the borrower's ability to manage monthly payments relative to their income.<br>

- **What is the business probem that your project is trying to solve?**<br>
The data given below contains information about past loan applicants and whether they ‘defaulted’ or not. The aim is to identify patterns which indicate if a person is likely to default, which may be used for taking actions such as denying the loan, reducing the amount of loan, lending (to risky applicants) at a higher interest rate, etc.

- **Steps involved in the EDA process :**<br>
  1. Importing all the necessary libraries for EDA
  2. Importing the csv file -> loan.csv
  3. Importing the meta-excel dictionary file for reference
  4. Setting to max rows and columns since the dataset contained (39717 records, 111 columns).
  5. All the empty columns were dropped after checking for the null values.
  6. The columns those had null values more than 50 % of their total records were also dropped after checking.
  7. All the object columns those had only single type of record were also dropped since they were not suitable to do comparative analysis during EDA.
  8. All the columns with unique IDs like were dropped since we are doing an overall data analysis and not individul ID wise. ['id', 'member_id', 'url']
  9. All the columns those had text description were also dropped since we are not working on any LLM model here. ['desc','title','emp_title']
  10. Based on our subject matter analysis we further decided to remove all the columns related to behavioural data attributes since such attributes are most relevant post loan approval (Althouh few of them can still be used for analysis its better to drop them for the simplicity of EDA analysis).
  11. For the simplicity of analysis the zipcode column was also dropped. Only the address column was used for analysis.
  12. The dataset was saved separately (in a different name --> df_cleaned_bivariate) till this step separately to continue with bivariate analysis later.
  13. Since we are trying to understand people who can default in future based on the existing loan_status record, the data of people those who are currently in the loan tenure and not yet fully paid or charged off are not useful. Therefore they were removed.
  14. The data type and format of the following columns were handled --> term, int_rate, emp_length. months/month was stripped from the 'term' column and the data type was converted from object to int. years, <, + and ' ' were stripped from the emp_length column and the data type was converted into float. The '%' string was removed from the int_rate column and the data type was converted from object to float.
  15. All the numeric columns were checked for outliers followed by removal of the outliers.
  16. For calculating the chargedoff proportion first we calculated:
    - Total = ChargedOff + Fully Paid
    - ChargedOff proportion = ChargedOf / Total <br>
This chargedoff proportion was then used for bivariate analysis. Futher for bivariate analysis we bucketed the columns [annual_inc', 'loan_amnt' , 'int_rate' , 'dti'] for creating further visualizations for our analysis.
  17. Please refer the ipynb file for all the univariate, bivariate and other analysis to understand in details.
  
<!-- You don't have to answer all the questions - just the ones relevant to your project. -->

## Conclusions
### Univariate Analysis
- **Loan Repayment**: Most people who take loans from the bank clear them off successfully.
- **Client Housing Status**: Clients living on rent are the most probable to default, followed by those who have mortgaged properties.
- **Loan Grades**: Grade B and Grade C clients have the highest chances of defaulting compared to other grades.
- **Sub-Grades**: The majority of clients who have been charged off belong to sub-grades B5, B3, B4, C1, and C2.
- **Loan Term**: Short-term loans are more likely to default compared to long-term loans.
- **Public Records**: Most clients charged off have no public record of bankruptcies. However, among the 308 records with bankruptcies, these clients show a higher probability of default.
- **State-wise Default**: Clients from the state of California (CA) have the highest chances of defaulting.
- **Loan Purpose**: Clients availing loans for debt consolidation are most likely to default.
- **Work Experience**: Freshers and clients with over 10 years of work experience are the most charged off.
- **Annual Income**: Clients earning between $20K and $60K are more prone to default. Upon further analysis, annual income between $0–$40K has the highest number of defaulters.
- **Loan Amount**: Most clients who defaulted had loan amounts between $3K–$5K, followed by $10K and $15K–$16K.
- **Interest Rates**: The majority of charged-off clients availed loans with interest rates ranging from 10% to 17.5%.

### Bivariate Analysis
- **Verification Status**: Loan applicants who have not been verified are more likely to default compared to verified or source-verified applicants.
- **Debt-to-Income Ratio**: Clients with a higher debt-to-income ratio are more likely to default.
- **Loan Amount vs. Default Rate**: Clients with higher loan amounts have increased chances of defaulting.
- **Interest Rate vs. Default Rate**: Higher interest rates correspond to a higher probability of default.

### Other Observations
- **Yearly Trends**: There is a yearly increase in the number of applicants being charged off. This could indicate either an increase in the number of new clients or inefficiencies in the bank's screening protocols for trustworthy loan applicants.
- **Behavioral Insights**:
  - Freshers may spend more than they earn, leading to an inability to pay debts on time.
  - Clients with higher work experience may opt for larger loan amounts and are potentially less cautious about timely repayment due to their financial stability.
- **Default Proportions**:
  - Clients with lower annual incomes have a higher default rate.
  - Clients availing loans with higher interest rates and larger loan amounts are at greater risk of defaulting.

<!-- You don't have to answer all the questions - just the ones relevant to your project. -->
## Technologies Used
- python version: 3.11.7 
- NumPy version: 1.25.2
- Pandas version: 1.5.3
- Matplotlib.pyplot version: 3.6.0
- Seaborn version: 0.12.2

<!-- As the libraries versions keep on changing, it is recommended to mention the version of library used in this project -->

## Acknowledgements
We would like to thank [Upgrad](https://www.upgrad.com/data-science-pgd-iiitb/?utm_source=PrudentAds&utm_medium=PrudentAds&utm_campaign=IND_LEADGEN_APP_prudentads_app_ALL_ALL_ALL_NewInitiative_India_Brandalliancesprudentads_1630&utm_content=PrudentAds&utm_term=PrudentAds&gad_source=1) to give us the opportunity to work on this project as a part of their course curriculum. 

## Contact
Created by [Ankit Srivastava](https://github.com/Ankit-Shrivastava-7) and [Anirudha Kumar Sahu](https://github.com/anirudhasahu92) 


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->