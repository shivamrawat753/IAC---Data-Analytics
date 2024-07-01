# Comprehensive Analysis of Student Interns' Academic and Career Data

## Project Overview

This project aims to conduct a comprehensive analysis of student interns to gain insights into the relationship between their academic performance, event participation, career aspirations, and factors influencing their success. The analysis will focus on understanding how economic background, competence, and expected salary are interconnected with students' academic metrics.

## Project Objectives

1. **Performance Goal:** Achieve a comprehensive analysis of the student dataset to identify key insights and correlations related to academic performance, economic background, and career aspirations.
2. **Time Goal:** Complete the analysis and reporting within the project duration of 2/4/8 weeks.
3. **Resource Goal:** Utilize the allocated data analysis tools, visualization software, and the project team's expertise efficiently within the defined budget.

## Business Case

The insights gained from this analysis can help improve student outcomes and better prepare them for the job market by highlighting areas for improvement and identifying key success factors. It addresses the absence of insights into the relationship between students' economic background, academic performance, competence, and expected salary.

## Goals/Metrics

1. Number of unique students included in the dataset.
2. Average CGPA of students.
3. Distribution of students across different graduation years.
4. Distribution of students' experience with Python programming.
5. Average family income of students.
6. Variation in CGPA across different colleges.
7. Outliers in the number of courses completed.
8. Average CGPA for students from each city.
9. Relationship between family income and CGPA.

## Expected Deliverables

- A comprehensive dataset analysis report.
- Visualizations of key metrics and distributions.
- Insights and recommendations based on the analysis.
- Identification of trends and correlations in the data.

## Scope

### Within Scope

- Analysis of existing student data.
- Visualization and interpretation of the results.
- Reporting on the findings.
- Providing actionable insights based on the analysis.

### Outside of Scope

- Collection of new data.
- Implementation of changes based on insights.
- Longitudinal studies beyond the provided data set.
- Individual student interventions.

## Project Team

- Data Analyst(s)
- Project Manager
- Subject Matter Expert (e.g., Education Specialist)
- Technical Support (for data management)

## Support Resources

- Data analysis software (e.g., Python, R)
- Data visualization tools (e.g., Tableau, Power BI)
- Access to the dataset and relevant documentation
- Statistical analysis tools

## Cost Allocation

- Software licensing for analysis and visualization tools
- Salaries for project team members
- Training and development for team members, if needed
- Miscellaneous expenses (e.g., data storage, report printing)

## Project Risks

- Data privacy and security concerns
- Incomplete or inaccurate data
- Misinterpretation of data analysis results
- Resource limitations (time, budget, personnel)

## Project Constraints

- Limited timeframe (2/4/8 weeks)
- Fixed dataset with no additional data collection
- Budget constraints for tools and personnel

## Project Assumptions

- The dataset provided is complete and accurate.
- Necessary resources (software, personnel) are available.
- Team members have the required skills for data analysis and reporting.
- Stakeholders are supportive and available for consultation.

## Basic Questions Answered in Analysis

1. **How many unique students are included in the dataset?**
2. **What is the average CGPA of the students?**
3. **What is the distribution of students across different graduation years?**
4. **What is the distribution of students' experience with Python programming?**
5. **What is the average family income of the student?**
6. **How does the CGPA vary among different colleges? (Show top 5 results only)**
7. **Are there any outliers in the quantity (number of courses completed) attribute?**
8. **What is the average CGPA for students from each city?**
9. **Can we identify any relationship between family income and CGPA?**

## Python Code for Analysis

The Python code provided in the script `student_data_analysis.py` handles the analysis of the dataset. Ensure that the dataset file `student_data.csv` is correctly placed and the necessary libraries are installed.

```python
import pandas as pd

# Load the dataset
df = pd.read_csv('/mnt/data/student_data.csv')

# 1. How many unique students are included in the dataset?
unique_students = df['Email ID'].nunique()
print(f"Unique students: {unique_students}")

# 2. What is the average CGPA of the students?
average_cgpa = df['CGPA'].mean()
print(f"Average CGPA: {average_cgpa:.2f}")

# 3. What is the distribution of students across different graduation years?
graduation_year_distribution = df['Year of Graduation'].value_counts()
print("Distribution of students across graduation years:")
print(graduation_year_distribution)

# 4. What is the distribution of students' experience with Python programming?
python_experience_distribution = df['Experience with python (Months)'].value_counts()
print("Distribution of students' Python programming experience:")
print(python_experience_distribution)

# 5. What is the average family income of the student?
average_family_income = df['Family Income'].mean()
print(f"Average family income: ${average_family_income:.2f}")

# 6. How does the CGPA vary among different colleges? (Show top 5 results only)
college_cgpa = df.groupby('College Name')['CGPA'].mean().sort_values(ascending=False).head(5)
print("CGPA variation among different colleges (top 5):")
print(college_cgpa)

# 7. Are there any outliers in the quantity (number of courses completed) attribute?
courses_completed_stats = df['Quantity'].describe()
print("Courses completed statistics:")
print(courses_completed_stats)
outliers = df[(df['Quantity'] < (courses_completed_stats['25%'] - 1.5 * (courses_completed_stats['75%'] - courses_completed_stats['25%']))) |
              (df['Quantity'] > (courses_completed_stats['75%'] + 1.5 * (courses_completed_stats['75%'] - courses_completed_stats['25%'])))]
print(f"Outliers in courses completed:\n{outliers[['Email ID', 'Quantity']]}")

# 8. What is the average CGPA for students from each city?
average_cgpa_city = df.groupby('City')['CGPA'].mean()
print("Average CGPA for students from each city:")
print(average_cgpa_city)

# 9. Can we identify any relationship between family income and CGPA?
income_cgpa_correlation = df[['Family Income', 'CGPA']].corr().iloc[0, 1]
print(f"Correlation between family income and CGPA: {income_cgpa_correlation:.2f}")
