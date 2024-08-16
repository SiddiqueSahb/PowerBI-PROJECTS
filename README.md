# PowerBI-PROJECTS
Project - Bicycle Company Quarterly Sales DashBoard
![Screenshot (3)](https://github.com/user-attachments/assets/cd44664c-8e5a-4516-ab54-b28d2b07f5e0)

Project - Trader Sales DashBoard

![Screenshot (2)](https://github.com/user-attachments/assets/ad1a6263-75ec-4248-9307-12cfd396604e)


1. Preparing the sales Excel data:
Prepare the sales data worksheet to ensure accuracy before integration into Power BI.
Understand the components of the sales data, such as individual sales per day and the corresponding gross amount.
Implementing formulas to determine the net amount by subtracting tax from the gross amount.

Calculate Gross Revenue
Total Tax
Calculate Net Revenue

Change the datatypes of columns 
Checking the column wise quality and distribution 

2. Design and Develop the Data Model:
 Construct a snowflake schema tailored for the data model.
 Establish and specify the relationships between various tables in the data model.
 Define a dedicated calendar table for temporal data analysis and reporting.


Tailwind Traders needs a report that shows the company’s worldwide sales and profits.


Step 1: Create a relationship between the tables
Step 2: Create new table using dax for time based analysis
CalendarTable =  
ADDCOLUMNS(
CALENDAR(DATE(2020, 1, 1), DATE(2023, 12, 31)),
"Year", YEAR([Date]),
"Month Number", MONTH([Date]),
"Month", FORMAT([Date], "MMMM"),
"Quarter", QUARTER([Date]),
"Weekday", WEEKDAY([Date]),
"Day", DAY([Date])
)

Establish relationship for new tables

 Sales in USD = 
ADDCOLUMNS(
    Sales,
    "Country Name", RELATED(Countries[Country]),
    "Exchange Rate", RELATED('Exchange Data'[Exchange Rate]),
    "Exchange Currency", RELATED('Exchange Data'[Exchange Currency]),
    "Gross Revenue USD", [Gross Revenue] * RELATED('Exchange Data'[Exchange Rate]),
    "Net Revenue USD", [Net Revenue] * RELATED('Exchange Data'[Exchange Rate]),
    "Total Tax USD", [Total Tax] * RELATED('Exchange Data'[Exchange Rate])
)

ESTABLISH RELATIONSHIP B/W SALES AND SALES IN USD TABLE

--------------------------------------------------------------------------------

Configure aggregations using DAX.

And Create sales and profit reports.


STEP 1 : creating measures
 In Power BI, a measure is a dynamic calculation that is evaluated in real-time during your report's 
 creation and viewing.
 Measures are used to perform calculations on your data, such as sums, averages,counts, or more 
 complex aggregations.
 They are essential for summarizing and analyzing data within Power BI reports and dashboards.


Step 1: Calculate Yearly Profit margin
Create a new measure for the Sales in USD table.

DAX USED
Yearly Profit Margin = 'Sales in USD'[Gross Revenue USD] / 'Sales in USD'[Net Revenue USD]
This calculation divides the Gross Revenue by the Net Revenue, and shows how much money is kept as profit from sales
after costs. 

Step 2: Calculate Quarterly Profit

DAX USED

Quarterly Profit = CALCULATE([Yearly Profit Margin], DATESQTD('CalendarTable'[Date]))

This calculation isolates the profit made in each quarter by using a time intelligence function, 
which filters the profit to each respective quarter.

Step 3: Calculate Year-to-Date Profit

This measure accumulates the profit from the first day of the fiscal year to the current date,
providing a running total of Tailwind Traders' profitability. 
This step provides a real-time snapshot of the company’s financial trajectory, allowing for comparison against 
the same period in previous years or projected targets.

Step 4: Calculate Median Sales 
Create measure of median
Median Sales = MEDIAN('Sales in USD'[Gross Revenue USD])

