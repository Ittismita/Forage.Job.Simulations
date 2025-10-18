## Data Analytics using GenAI

#### Scenario
As an AI transformation consultant, have been tasked with helping Geldium Finance, a financial services company, reduce its high credit card delinquency rate by performing advanced analytics and building AI/ML models with the assistance of GenAI. 

Geldium, a financial services provider specializing in digital lending and consumer credit, has observed an increase in credit card delinquency rates, with more customers missing payments beyond the 30-day late payment threshold. To improve risk management and customer engagement, they have engaged Tata iQ(us) to develop an AI-powered predictive solution that helps identify at-risk customers and recommend appropriate interventions.

The head of Geldium’s Collections team wants to improve how they assess repayment risk and prioritize outreach efforts. Currently, their approach relies on historical trends and manual case handling, which limits efficiency. 

They are looking for a solution that can:
1. Use AI-driven insights to help predict which customers are likely to miss payments.
2. Support the Head of Collections with targeted intervention strategies to reduce delinquency.
3. Ensure fairness and transparency in AI-driven risk assessments while aligning with industry practices.

#### Task
1. EDA, risk profiling and quality assessment:
Key Objectives:
- Review the provided dataset and assess its structure, completeness, and key attributes, and then identify any missing or inconsistent data points that could affect predictions.

- Use GenAI-assisted tools to generate insights while ensuring data confidentiality and avoiding the exposure of sensitive financial information.
  
- Summarize the patterns, anomalies, and risk indicators that should be considered in later stages of the project in a report.

   - #### Steps:
     1. Reviewed dataset and identified key insights
        1. Understand Dataset - Structure of data
           - Total datapoints - 500
           - Column Descriptions - Total Columns - 19
             - Numerical Columns - 8
               - Age - Customer's age in years. (Numerical)
               - Income - Annual income of the customer in USD. (Numerical, may contain missing values)
               - Credit_Score - Customer's credit score, typically ranging from 300 to 850. (Numerical)
               - Credit_Utilization - Percentage of available credit currently in use. (Numerical, 0-100%)
               - Missed_Payments - Total number of missed payments in the past 12 months. (Numerical)
               - Loan_Balance - Total outstanding loan balance in USD. (Numerical)
               - Debt_to_Income_Ratio - Ratio of total debt to income, expressed as a percentage. (Numerical, 0-100%)
               - Account_Tenure - Number of years the customer has had an active account. (Numerical)
       
            - Categorical Columns - 11
               - Customer_ID - Unique identifier for each customer. (Categorical)
               - Delinquent_Account - Indicator of whether the customer has a delinquent account. (Binary: 0=No, 1=Yes)
               - Employment_Status - Current employment status (e.g., 'Employed', 'Unemployed', 'Self-Employed'). (Categorical)
               - Credit_Card_Type - Type of credit card held (e.g., 'Standard', 'Gold', 'Platinum'). (Categorical)
               - Location - Customer's region or city of residence. (Categorical)
               - Month_1 to Month_6 - Payment history over the past 6 months: 0 = On-time, 1 = Late, 2 = Missed. (Categorical) - spread over 6 columns
             
          - Missing values present in the dataset -
            - Income	- 38 - 7.6%
            - Loan_Balance - 29 - 5.8%
            - Credit_Score - 2 - 0.4%
            - Credit_Utilization - 1 - 0.2%
           
          - Inconsistencies in data -
            - 'Employment_Status' Column - the category "employed" had 3 different forms in the data - "Employed", "employed" and "EMP". Hence standardized all to "employed".
           
          - Outliers in the dataset - 
            - Through IQR method, no outliers were detected in any column.
 
          - Duplicates - NADA!!!
            
          - Top 3 variables that can predict delinquency
            - Missed_Payments
            - Debt_to_Income_Ratio
            - Credit Utilization
            
          - Key Patterns/Anomalies in the dataset
            - Primary pattern - Behavioral financial metrics are stronger predictors of delinquency than static attributes.
            - Key Predicitve Patterns - Customer Financial Habits => Likelihood of becoming Delinquent.
            - How a person manages their finances is more indicative of risk than static figures like income or credit scores.
                       
        2. Filled missing values
           - Found reason for missingness => imputation/deletion/synthetic data generation.
             - Possible reasons could be - logging/data entry errors, optional form fields, data integration or merging errors, system glitches
           - Imputation strategy - median for Income and Loan_Balance
           - Drop the rows containing missing values in Credit_Score and Credit_Utilization

        3. Detect patterns and risk factors in the dataset
           - Relationship between variables and delinquency outcomes
             - There's no strong linear correlation between any two numerical variables.
             - Income and Loan_Balance have weak positive correlation. This is intuitive as people with high income will be able to take on larger loans.
             - Weak negative correlations between:
               - Credit_Score and Missed_payments - People with more missed payments tend to lose scores.
               - Credit_Score and Credit_Utilization - As utilization go up => more available credit is used => score goes down.
           - Delinquency Rate - Prevention: "What percentage of people within a specific group(Employment_Status) are delinquent?" This tells us the *risk* associated with that group => Unemployed individuals had the highest risk (35.1% rate).
           - Delinquency Contribution - Mitigation: "Of all the people who are delinquent, what is the breakdown?" This tells us about the volume or composition of your delinquent population => The "Employed" group made up the largest portion of delinquent accounts (37.7% of the total).
           - The dataset is significantly imbalanced(skewed) based on the "Delinquent_Account" column. There are far more non-delinquent customers(74%) than delinquent ones(26%).

2. Predictive Modelling
Key Objectives:
- To predict which customers are at risk of missing payments using AI, so that Geldium can take proactive steps to reduce delinquency.
  
- To develop a model that helps support Collections team in prioritizing outreach and intervention strategies.

- Evaluate model accuracy and reliability while considering bias, explainability, and fairness—all essential for making responsible AI-driven decisions in financial services.

   - #### Steps:
     1. Selecting the right model type:
        4 models were trained on this data to come up with the best one:
        with their performance evaluated using different metrics. The AUC-ROC score is the most important metric here. It measures how well a model can distinguish between delinquent and non-delinquent customers. A score of 1.0 is perfect, while 0.5 is no better than a random guess.
     2. Evaluating model performance:
         
         |Model	             |Accuracy|Precision|Recall|F1-Score|AUC-ROC|
         |---------------------|--------|---------|------|--------|-------|
         |Decision Tree        |76.8%   |0.58     |0.54  |0.56    |0.71   |    
         |Logistic Regression	 |79.8%	 |0.65	  |0.54	|0.59	   |0.77   |
         |Random Forest	       |81.8%	 |0.71	  |0.58	|0.64	   |0.83   |
         |XGBoost Classifier	 |83.8%	 |0.75	  |0.62	|0.68	   |0.85   |
    
        As we can see, the XGBoost model outperformed the others.
        The XGBoost model's AUC score of 0.85 was a strong result, indicating it has a high degree of accuracy in identifying which customers are likely to miss payments.

     
        
    
     


        
#### Learnings
   - Understand customer risk factors for delinquency:
        Analyze financial and behavioral indicators => whether a customer is likely to miss payments => take steps for early internvention => reducing losses and improving repayment outcomes.
     
        a. Payment history – Customers with a history of late or missed payments are more likely to default.
        b. Credit utilization rate – High usage of available credit can indicate financial stress and potential repayment issues.
        c. Debt-to-income (DTI) ratio – A high DTI suggests a customer may struggle to manage their financial obligations.
        d. Recent credit activity – A sudden increase in new credit accounts or loan applications may signal financial instability.
        e. Employment and income stability – Frequent job changes or inconsistent income can contribute to a higher risk of missed payments.
        f. Demographic trends – While AI models must avoid bias, certain patterns (e.g., younger customers with limited credit history) may require additional analysis.

   - How to leverage synthetic data generation to enhance datasets
     - Help fill gaps, simulate scenarios, improve data quality.
     - Artificially generated data => mimicking real world data patterns
     - Using statistical models like Monte Carlo simulations, bootstrapping, and probabilistic modeling or AI - driven techniques
 






