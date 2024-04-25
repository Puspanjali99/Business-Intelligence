# Deloitte Case Study

### Dashboard Link : https://github.com/Anirudhbangari/Power-Bi/blob/main/int1l.pbix
## Problem Statement

This dashboard helps  as a collective term to refer to a broad range of economic services provided
by the ﬁnance industry, which encompasses a broad range of organizations that
manage money, including credit unions, banks, credit card companies, insurance
companies, consumer ﬁnance companies, stock brokerages, investment funds A
banking domain is comprised of all the components needed to run a ﬁnancial service
end-to-end. It covers the transaction and distribution process; the ways in which
customers interact with the system, products, and services the organization oﬀers; and
the technology involved.



### Steps followed 
First, for all three files—CPI, exchange rate, and merchandise exports—any missing values should be filled using backfill and forward fill methods. This is because these variables, namely CPI, exchange rate, and merchandise exports, often exhibit a growing trend or remain stable over time. Therefore, the most suitable approach to impute missing values is to use the nearest available value.

    After in Power BI

- Step 1 : Load data into Power BI Desktop, all dataset is  csv file.
- Step 2 : Transform all data table unpivot other(other than period column) in transform option and name new column country
- Step 3 : Than name period column in annual data of all file
- Step 4 : Split period column in monthly data of all file year and month wise name respectively
- Step 5 : Merage all data annually and monthly wise
        
Snap of new annual data ,
![annuAL](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/ae83814b-5427-4ada-bbfe-336a49ef7410)

Snap of new monthly data,
![Monthly](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/2c5f7e1a-b32b-4ff4-9bb9-b9e3ccbd9054)

- Step 6 : After applying Dax querry to get annualy and monthly growth rate of country according to Cpi,Exchange rate and Export Merchandise
  
Following DAX expression was written for the annualy growth of cpi
Percentage Growth of CPI = 
VAR PreviousYearCPI = CALCULATE(MAX('Merge all file annual'[CPI_value]), 
                    FILTER('Merge all file annual', 
                           'Merge all file annual'[Country] = EARLIER('Merge all file annual'[Country]) && 
                           'Merge all file annual'[Year] = EARLIER('Merge all file annual'[Year]) - 1))
RETURN
IF(ISBLANK(PreviousYearCPI), BLANK(), ('Merge all file annual'[CPI_value] - PreviousYearCPI) / PreviousYearCPI * 100)

Exchange rate and Export Merchandise DAX expression also same apart from column name 

-snap after apply DAX expression

![Screenshot 2024-04-22 201224](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/1aa6e29f-42dd-4032-bdf2-ae4e71107782)

Following DAX expression was written for the monthly  growth of cpi
CPI_Growth(%) = 
VAR CurrentCPI = [Cpi_value]  // Replace 'YourCPIColumnName' with the actual name of your CPI column
VAR PreviousCPI = 
CALCULATE(
    MAX([Cpi_value]), 
    FILTER(
        ALL('Merge all file monthly'), 
        'Merge all file monthly'[Country] = EARLIER('Merge all file monthly'[Country]) &&
        'Merge all file monthly'[Month] = EARLIER('Merge all file monthly'[Month]) - 1 &&
        'Merge all file monthly'[Year] = EARLIER('Merge all file monthly'[Year])
    )
)
RETURN
IF(
    ISBLANK(PreviousCPI) || PreviousCPI = 0, 
    BLANK(),
    ((CurrentCPI - PreviousCPI) / PreviousCPI) * 100
)


Exchange rate and Export Merchandise DAX expression also same apart from column name 
-snap after apply DAX expression

![Screenshot 2024-04-22 201504](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/b3b41e34-7d4b-495c-84d2-151a1c85a08d)


- Step 7 : After that card are used for show growth percentage accordingly to monthly and annualy of cpi,Exchange rate and Export Merchandise of
  of different country
- Step 8 : Slicer used Yearly and Country in Annualy page
- Step 9 : Slicer used Yearly ,Country and Monthly in Monthly page
- Step 10 : Use Line Chart to study how one variable impact other variable E.g How export merchandise impact the exchange rate
- Step 11 : Use map to view location of country
  
# Snapshot of Dashboard (Power BI Service)
    Snap of dashboard of annualy
![page1](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/43c22c72-ea2b-4d7c-9945-31388030a084)

  Snap of dashboard of monthly
  ![page2](https://github.com/Anirudhbangari/Power-Bi/assets/35010033/f5485981-2dc5-4f1c-acd8-ef4595f4568c)


# Insights

Two pages report was created on Power BI Desktop .

Following inferences can be drawn from the dashboard overall for all country and all year;

### [1] Economic Stability Post-2000:
The stabilization of exchange rates post-2000 suggests that the global economy or the economies of the countries in your dataset became more stable or were influenced by factors that reduced volatility in exchange rates.

### [2] Inflationary Pressure: 
The CPI growth rate of 10.87% indicates significant inflationary pressure across the countries in your dataset. High inflation can impact purchasing power, investment decisions, and overall economic stability.
### [3] Export-Led Growth: 
The steady growth in export merchandise indicates that the export sectors of these countries have been strong contributors to economic growth. This suggests that these countries have been successful in exporting goods and services to foreign markets, potentially boosting their economies and creating jobs.
### [4] Exchange Rate as a Reflection of Economic Health: 
The fluctuating exchange rates before 2000 followed by a more uniform growth pattern suggests that exchange rates can be a reflection of the overall economic health and stability of a country or group of countries.

    In conclusion, dashboard provides valuable insights into the economic performance of various countries over time. Understanding these trends can help         policymakers, investors, and analysts make informed decisions about economic strategies, investments, and risk management.
   
