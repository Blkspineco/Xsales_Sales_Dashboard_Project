# Xsales Financial Database and Dashboard

# Overview
This project was done to develop a Dahsboard for Xsales fictional company to improve my exploratory analysis, dax measures complexity, dashboard presentation, use of different graphs to support business ideas, focusing on comparing the sales development throughout 2022 - 2024, Sales representatives performance and customers habits. It includes sales across three years, customers purchase habits, sales representatives behaviours and stores performance in various states across the US. The database from which I was able to make this project was given by the educational insitute Daxus Latam, it was all given in an xlsx file, then by doing certain analysis and setting the best graphs to view the business sales, sales reps performance and clients spending habits. 

# Project requirements
1. General Analysis of company revenue by region and period.
It is considered crucial to evaluate a given period in relation to previous years, as well as to analyze the revenue contribution of the regions with the highest sales.
Additional desired analyses: Profit, Profit Margin (%), Average Daily Revenue, and Average Transaction Value.
The dashboard must allow filtering by selected period and region.

2. Salesperson view: revenue analysis by salesperson and period.
In addition to comparing revenue from the current period with that of the previous year,
an analysis of salesperson performance is required, as shown in the following example:
Compare the selected salesperson with the company-wide average and with the top 3
salespeople in terms of revenue and number of orders.
Create a ranking showing the top 3 salespeople by revenue.
The dashboard must allow filtering by selected period and salesperson.

3. Customer View: In this dashboard, you must analyze the structure of the company's customer portfolio.
Status Analysis: Each customer must be categorized based on their status.
Based on the time elapsed between the last purchase and the current date: if the difference is less than 45 days, the customer should be classified as "Active"; between 45 and 90 days, as "Contact Needed"; and 90 days or more, as "Inactive."
Current Date: Use the date of the company's most recent sales record. Profile analysis: Since the only information the company has about its customers is their name, it will be necessary to use purchase record data to create a profile characterization for each customer.
Note: A suggested approach is to use the average annual income of residents in the neighborhood where the purchase was made (information available in the "dLocal - Average Income" table).
New customer analysis: Evaluate the number of new customers for this company over the years. Count only those with no prior purchase records as new customers.
In addition to the general information described above, a query by customer name is required, containing: consumption information, last order, total orders, average order value, and the region(s) where the customer made purchases.
The dashboard must allow filtering by selected time period and by customer name.

# Project Workflow
```
Load xlsx file
        |
Explore the data
        |
Data Preparation
        |
Initial Dax measures for initial kpi's and overview of revenue
        |

```

# Skills & technologies
Technologies: Power BI, DAX
Skills: Data Analysis, data visualization

# Dashboards
The initial dashboards show the revenue for the years '22 to '24, mainly the idea was to compare the current year(2024) vs last year, also the top 5 in revenue for cities, states and the profit. It shows a minimap that has a conditional format that shows a more intense green for the state with the highest sales, also there's a filter for the period and the location. In the section **Interactive Dashboard** you can go to and interact with the dashboard yourself.
![Dashboard_1](Images/Dashboard_1.1.png)
*Dashboard of General Analysis of company revenue by region and period* 


![Dashboard_2](Images/Dashboard_1.png)
*Dashboard of Salesperson performance*

![Dashboard_3](Images\Dashboard_3.png)
*Dashboard of Customer portfolio*

# Data model diagram
To achieve the desired requirements, I opted to create a dimensional model consisting of 5 dimension tables and one fact table of sales as seen below:
![Diagram](Images/Diagram.png)

# DAX Measures
To get started on measures I went for the basic ones like making a calendar table with dax
```sql
dCalendario = 
          VAR V_min_date = MIN(fventas[fecha_compra])
          VAR V_Calendario = FILTER(
                                  CALENDARAUTO(),
                                  YEAR([Date])>=YEAR(V_min_date)
          )
          RETURN ADDCOLUMNS(
                            V_Calendario,
                            "Month",FORMAT([Date],"mmm"),
                            "Month_name",MONTH([Date]),
                            "Month_year",FORMAT([Date],"mmm") & " " & FORMAT([Date],"YY"),
                            "Trimestre","Q" & FORMAT([Date],"Q"),
                            "Dia_semana",FORMAT([Date],"DDD"),
                            "Año",YEAR([Date]))
```

# Key Insights

# Interactive Dashboard
