# 
# Botanicals Co. Power BI Report 

### Report Link : https://app.powerbi.com/view?r=eyJrIjoiMDA1MmQ0ZTYtMmRlYy00MjFjLWFmY2MtNDc4NWFmMGY4NGIzIiwidCI6IjI1MWJhYTNiLTIxODUtNGExYi04MzgzLWUyMGUwNjZkMDllOSIsImMiOjEwfQ%3D%3D



## Business Statement

To analyse the sales data provided to better understand the company performance and how it has changed in the past 3 years.  


### Steps followed 
#### Extract, Load, Transform
- Step 1 : Load data into Power BI Desktop, dataset is a xls file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Noticed duplicates in the key columns in all 3 queries imported, removed the duplicates. Noticed a null value in the main facts table, the Null was changed to a 0. 
- Step 4 : Checked column headers for proper data type formatting as well as spelling errors.
- Step 5 : Created a date table to reflect the full range of dates available.
- Step 6 : In the model tab, the relationships were configured (One-to-Many) from dimension tables to fact table.

#### Calculated Measures and Slicer Configuration
- Step 7 : A new table was created to hold all the calculated measures in one place.
- Step 8 : A set of base measures/key metric (Sales, Quantity, Gross Profit) was created for later use.
- Step 9 : Created a new table to hold the slicer labels for each key metric.
- Step 10 : In order to do a year to year performance comparison, YTD and PYTD measures were created.

""

    PYTD_Gross_Profit = 
        CALCULATE(
            [Gross_Profit], 
            SAMEPERIODLASTYEAR(date_table[Date]), 
            date_table[PYend]
            )


- Step 11 : The above PYTD formula was reused to formulate the PYTD for Sales and Quantity.
- Step 12 : The YTD measures were also created with the following DAX formula:-
  
""

    YTD_Gross_Profit = 
        TOTALYTD(
            [Gross_Profit], 
            Fact_sales[Date_Time]
            )

- Step 13 : The above YTD formula was also reused to formulate the measure for YTD Sales and Quantity. 
- Step 14 : In order for the slicers to function dynamically as per my intention, a measure was for PYTD and YTD were created for the slicers.

""

    PYTD_SLICED = 
    VAR selectedvalues = SELECTEDVALUE(Slicer_values[Values])
    VAR results = SWITCH(
        selectedvalues,
        "Sales", [PYTD_Sales],
        "Quantity", [PYTD_Quantity],
        "Gross Profit", [PYTD_Gross_Profit],
        BLANK()
    )
    RETURN
    results


    YTD_SLICED = 
    VAR selectedvalues = SELECTEDVALUE(Slicer_values[Values])
    VAR results = SWITCH(
        selectedvalues,
        "Sales", [YTD_Sales],
        "Quantity", [YTD_Quantity],
        "Gross Profit", [YTD_Gross_Profit],
        BLANK()
    )
    RETURN
    results

- Step 15 : Gross Profit % and YTD vs PYTD measures were also created for future use. 

#### Visualisation
- Step 16 : A slicer visual was created and all created measures were tested by placing them into a table for temporary testing.
- Step 17 : Cards and slicers were created with the ability to display YTD and PYTD data.

 ![Snap_slicer](https://github.com/user-attachments/assets/bbc80f5a-f414-4659-8668-c9410ff29b2c)

 ![Snap_1](https://github.com/user-attachments/assets/bafff096-2df8-4b36-98be-c0e70f7842ab)

- Step 18: A waterfall chart with the ability to drill down from the month to the country and product with the dynamic ability for the values to be selected by the slicers was created along side other visuals such as a heatmap to identify the worst performing 10 countries alongside a column/line combination visual and a scatter plot visual.

- Step 19 : The theme for the project was selected and colours on the visuals were adjusted via conditional formatting to allow for a cohesive look.

- Step 20 : Some of the headers were created via a measure inserted into the conditional formatting section in order for the title to change as per the selected slicer value.

"

    Waterfall_Title = SELECTEDVALUE(Slicer_values[Values]) & " YTD vs PYTD | MONTH - COUNTRY - PRODUCT"

    Scattter_Title = "Product (Family-Group-Name) Profitability | " & SELECTEDVALUE(Slicer_values[Values])

    Project_Title = "Botanicals Co. Performance Report " & SELECTEDVALUE(date_table[Date].[Year])


- Step 21 : The other visual details were then adjusted and axis labels amended accordingly.

- Step 22 : The final report is as per the following image:-

![Snap_3](https://github.com/user-attachments/assets/433cfac9-7c4e-4b76-a56d-6f2aa6a35806)
        

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the report;

### YTD vs PYTD results

- The gross profit and sales have been falling year on year for the past 2 years.
- The largest decrease in YoY sales was February 2023 with a drop of $350,000 in sales. The largest contributor to this drop is China contributing to a $260,000 reduction YoY. 
- For the 2024 period, the largest contributing month to the drop in both sales and gross profit would be April and the largest contributor for this drop is Canada. However, as per the drilled down waterfall chart, it can be noted that there is a drop in sales for almost all countries during this month. 
- Based on the visual of the bottom 10 performing countries, it can be inferred that Canada shows the largest drop in YoY Sales, Quanty and Gross Profit. Other countries in the bottom 10 should also be monitored. 
- Despite China being the largest contributor in drop in YoY Sales in 2023, it was noted that the 2024 year showed a increase in their sales compared to the year before. 
- Certain product family such as Asteraceae and Fabaceae seem to the largest contributor in terms of sales and has a decent gross profit margin. Some product families such as Portulacaceae and Pedaliaceae seem to not sell well and yet has a rather low profit margin. 
           

### Recommendations

- Perform a deeper dive into the bottom 10 performing countries. Focus on the bottom 3 in sales which are Canada, Colombia and Croatia. Identify whether changes are needed to approach these markets. 
- Find out the potential external causes of the drop in sales. Is it a global drop in sales for the industry or is it localised to certain countries or is the drop in sales only affecting Botanicals Co. 
- Put greater focus on the products which have a high turnover with average to above average Gross Profit %. 
- Consider phasing out certain products which have a low gross profit % and does not sell well. 
