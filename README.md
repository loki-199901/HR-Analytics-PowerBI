# HR Data Analytics

# Overview
This project leverages HR data to uncover valuable insights into employee retention, attrition patterns, and factors shaping workforce dynamics. By employing data transformation techniques and DAX calculations in Power BI, the dashboard provides a comprehensive analysis of employee tenure, attrition rates, salary distribution, and training hours. These insights aim to help organizations make data-driven decisions to improve employee satisfaction and retention.

##Key Features

**Total Employees**: Provides the total count of employees within the organization.

**Employees Left**: Identifies the number of employees who have left the company, filtered by Attrition = "Yes".

**Attrition Rate**: Calculates the percentage of employees who left the company in relation to the total workforce.

**Years Category**: Segments employees into tenure categories: 1-3 years, 3-5 years, 5-10 years, 10-15 years, and 15+ years.

**Promotion Category**: Groups employees based on the time since their last promotion: less than 1 year, 1-3 years, 3-5 years, and 5+ years.

**Salary Insights**: Analyzes attrition trends across various salary brackets, identifying areas for potential improvements in compensation.

**Training Insights**: Explores the relationship between the number of training hours received and attrition rates, highlighting the importance of professional development.

##Data Transformation & DAX Calculation

**1. Total Employees:**
Counts the total number of unique employees based on EmpID.

TotalEmployees = COUNT(HRTable[EmpID])

**2. Employees Left:**
Counts employees who left the company, filtered by Attrition = "Yes".

EmployeesLeft = CALCULATE(COUNT(HRTable[EmpID]), HRTable[Attrition] = "Yes")

**3. Attrition Rate:**
Calculates the attrition rate by dividing the number of employees who left by the total number of employees.

AttritionRate = DIVIDE([EmployeesLeft], [TotalEmployees], 0)

**4. Years Category:**
Categorizes employees based on the number of years they have been with the company.

YearsCategory = SWITCH(
    TRUE(),
    HRTable[YearsAtCompany] >= 1 && HRTable[YearsAtCompany] < 3, "1-3 years",
    HRTable[YearsAtCompany] >= 3 && HRTable[YearsAtCompany] < 5, "3-5 years",
    HRTable[YearsAtCompany] >= 5 && HRTable[YearsAtCompany] < 10, "5-10 years",
    HRTable[YearsAtCompany] >= 10 && HRTable[YearsAtCompany] < 15, "10-15 years",
    HRTable[YearsAtCompany] >= 15, "15+ years",
    "Unknown"
)

**5. Promotion Category:**
Categorizes employees based on the number of years since their last promotion.

PromotionCategory = SWITCH(
    TRUE(),
    HRTable[YearsSinceLastPromotion] < 1, "Less than 1 year",
    HRTable[YearsSinceLastPromotion] >= 1 && HRTable[YearsSinceLastPromotion] < 3, "1-3 years",
    HRTable[YearsSinceLastPromotion] >= 3 && HRTable[YearsSinceLastPromotion] < 5, "3-5 years",
    HRTable[YearsSinceLastPromotion] >= 5, "5+ years",
    "Unknown"
)

##Insights & Analysis

**1. Attrition Rate:**
The attrition rate for employees is 16.12%, with a higher rate among those with less than 1 year of tenure. Employees aged 25-35 are most likely to leave the company.

**2. Role-Based Attrition:**
Sales Executives and Laboratory Technicians have the highest attrition rates, indicating a need for role-specific retention strategies.

**3. Salary & Attrition:**
Employees earning up to 5K show a higher attrition rate. A review of compensation in these salary bands could help improve retention.

**4. Training Hours & Retention:**
Employees who received more than 400 hours of training show a higher retention rate. This highlights the importance of professional development in reducing turnover.

**5. Recommendations:**
Investigate the causes of high attrition within the first year of employment.
Improve salary competitiveness for employees in lower salary bands.
Develop targeted retention strategies for employees aged 25-35.
Review the effectiveness of training programs, particularly for high-turnover roles.
