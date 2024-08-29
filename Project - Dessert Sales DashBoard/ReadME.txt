Chocolate Sales Analytics

Sales Boxes costs and profits

Sales Person and Product Perform
Low Box Shipment analysis
MoM/YoY changes

Schema USed
Star Schema


Key Measures:
Total Sales
Total Boxes
Total Shipments
Total Cost
Total Profit
Calculating Profit %
Any box less than 3 then Low Box Shipment (LBS) means sending sample 
MOM and YearonYear Changes

1.Creating Measure
2.Finding Total Cost per Shipment by cost per box * no of boxes
3.Using Power Query Using Calendar Table performing Time Series Anlaysis and from Date extracting Year,Month,Day,Week
4.Calculating prevMonth Sales
5.Calculating MoM changes (Box,Sales,Cost,Shipment)%
 MoM Sales Changes % = 
    var this_month = [Total Sales]
    var prev_month = [Total Sales prevMonth]
return
    DIVIDE(this_month-prev_month,prev_month)




Visuals
1. using cards visual for key measures,for profit margin using gauge charts
2. Performing Conditional Formatting Based on -ve No on Cards Visual
3. Line Chart for Trend Analysis
4. Adding Parameter as Field name (Measure Selector) to Line Chart 
   It will create Slicer New , Now Based on Slicer Selection Line Chart Must reflect on Changes, So on 
   Line Chart Adding Y axis Data as Measure Selector
5. Formatting Slicer i.e On Selection Font Size increases (Check on Visual -> Callout Values)
6.Shipment on Range of Boxes (creating Histogram with 20 bins)
7.Using Zoom Slider 
8.LowBoxShipment gauge indicator
9.Creating Measure for Sales Person Profit Target 
10.Creating a Table of Sales Person along with total sales , profit % , profit target
11.Formatting the Table at global level and setting global font size
12.Row padding and Applying Conditional Formatting to Profit target Indicator in Table
13.Creating BookMark by Selection panel on Clicking View
14.Change name in Selection and Add BookMark by repective names and then in Visualization Pane setup Action
  for repective labels
15.Change Setting in BookMark , so that it doesn't store data and on toggle it must display the correct data
16.Adding Slicer to filter the data based on Demography




