# Excel-Clothing-Store-Analysis
## Project Information
Modern Traditional Clothing Store is an online clothing store based in India, which sells womens and mens clothing through online channels such as Amazon, Myntra and Ajio. The executives of Modern Traditional Clothing Store have requested us, the Data Analysts employed by the store, to create an annual sales report for 2022 in the form of a dashboard using Microsoft Excel. Executives say this report will assist them with understanding their customer base and how to grow their sales in 2023. We have been given 8 questions by the executives (below), which we need to address through our analysis. 

1. Compare the sales and orders using a single chart
2. Which month had the highest sales and count of orders?
3. Who generated the most sales, women or men?
4. What are the different statuses of orders?
5. Which are the top 10 states contributing most to sales?
6. What is the relationship between age and gender based on number of purchases?
7. Which channels are contributing the most to sales?
8. Highest selling category?

The Data Engineers for the store have provided us with the dataset for 2022 in the form of an Excel file, which we'll be using for our analysis.

In this case, we have been given the dataset and the questions we need to answer, however, a lot of the time in the real world this will not be the case. Data Analysts will be given a business problem and it will be upto us to decide which data we need, where to source the data from e.g. internally from within the company database or from an external source and which questions should be addressed to help solve the business problem. In this case, we haven't been given mock ups or example dashboards, however, the executives have mentioned that we're free to design the dashboard how we would like, as long as the information addresses the questions and is clearly and easily conveyed. 

In this project, we will begin with data cleaning, then move onto data processing and analysis, and finally, dashboard creation.

## Data Checking
The very first thing we will do, is create a copy of our dataset. Never work on the original dataset and alter the data, if something goes wrong and is not able to be reversed, we've just corrupted our data and we're in trouble. We will also create a document, where we'll document this task. It's important to document all the tasks you undertake in a workplace, so you have a record and can refer back to it in the future when needed such as during meetings with managers and executives. We will save all the above in a secure folder.

We will now check over our data, this can be viewed as the analysis before the analysis. We have been given data by the engineers, who are highly educated and qualified professionals, however, as best practice, we have to make sure the data is appropriate for our task. 

Upon opening the dataset, we can see certain columns providing demographic data such as gender and age. We also have columns such as the ship city column providing geographic data. We can also see columns which provide us with cusotmer purchase information such as what channels are being used to make purchases, what categories are being purchased from, which sizes and the quantities and price of each item. Additionally, there are also ID columns such as customer ID and order ID, as well as an index, which can be viewed as keys. These are unique identifiers assigned to a particular piece of information such as customer ID or order ID. In this dataset an index column provides a unique identifier for each row, where each row denotes the whole of a single order or a part of an order. 

From this data, we can already see that we have the information to help us understand the stores customer base. Having demographic, geographic, behavioural and psychographic data can help with customer profiling and in gaining a deeper understanding of the customer. This information can then be used to drive business decisions such as marketing based decisions e.g. how to market to each segement of the customer base and how much to market and inventory based decisions e.g. which products should be stocked more or less.

Lets move onto data cleaning to make sure the data is in good shape before analysis.

## Data Cleaning
Data cleaning is an **crucial** process, as we want our data to be in the best possible state, free from as much "rogue data" as possible. Rogue data being, incomplete, inaccurate, irrelevant, corrupt or incorrectly formatted data. Having accurate, complete, relevant and correctly formatted data will make sure our analysis is reliable and will make other tasks easier such as future analyses.

Lets start by checking for blanks, duplicates and inconsistencies within our data. To check for blanks/nulls in our dataset, we will highlight all the data by pressing ctrl+A or double clicking the triangle on the left corner next to column A, then we'll utilise the go to special function by pressing F5, click blank, OK and Excel will begin scanning the dataset. We've received a "no cells were found" from Excel, which means so there are no blanks in our dataset. If in the case we did get nulls, we would have to figure out what to do with these nulls. Sometimes it's just a matter of looking at the data surrounding it and filling in the null. For example, you may have a customer who's purchased two items, these will be shown in two rows, each with an order ID and customer ID value. Lets say the order ID was missing for one of the rows, by looking at the other row and seeing that the Order ID is the same, then it's clear that the customer ID will be the same too. In other cases, you may have to decide whether to use the mean, median, mode or other method for imputation. Generally, the mean is the most common method for imputation of numeric data, but if there are outliers it won't be the best option as outliers can heavily skew the mean in either direction. Where there are outliers, the median is a better option. The mode is more appropriate for categorical data. These are not the only imputation methods, other methods include forward and backward fill for time series data and interpolation such as linear interpolation. However often times the clues aren't within the dataset and we have to either liase with other stakeholders e.g. Data Engineers to see if the data can be retrieved and/or discuss with managers and executives to see how to handle the missing values. 

We'll also have a look at our index column to see if the unique row identifiers are in sequential ascending order. To do this, we will use the formula: IF(OR((A2+1=A3),(A2-1=A1)),"Sequential","Not Sequential")
Here we're asking Excel to output "Sequential" if a cell plus 1, equals the the value of the cell below. If this condition is not met, Excel will output "Not Sequential". After running the formula, we will go to Data and add a filter to the column, so we can see the distinct values. Here we can only see "Sequential", meaning that the values of the column are in ascending sequential order. If there was a "Not Sequential" shown, we would use the filter to find where this occurred and correct the issue. It's important we correct any errors with a primary key column as these keys are used to connect tables with one another. 
![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/95185f25-7e03-4046-a64b-89ac387b51d4)

We will now go column by column checking for any issues, once again, we'll be looking out for any abnormal values, these could be an integer that's much lower or higher than the expected range or a repeat of value but with a spelling error etc.

Order ID: 
The Order ID column contains numeric characters in a particular format, with 3 numeric characters followed by a dash and 7 numeric characters, followed by a dash and 7 numeric characters again. Upon adding a filter and scanning through the disctinct values in the filter
Customer ID:
- Contains numeric characters for the customer ID, using the same process of running a filter and scanning through, no issues or abnormalities standout.
Gender:
- Already on first glance, we can see that there's "Women", "Men" and "W", indicating that genders have been denoted with both the word and the first letter of the gender. We want to denote using just one method, here we'll denote the genders using the words "Men" and "Women" and replace any "W" and "M" with these. To do that, we will filter for "M" and "W" and run the find and replace function and replace these with the appropriate the gender.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/c6c52777-20c4-42a7-956b-37677bd738ec)
Before

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/a0f7f1e0-30fd-4c4e-915b-776d542e6eed)
After running find and replace

Age:
Numeric characters/integers. We will run a filter again and check for any abnormal values. For example, if the value 6 showed, we would know for certain that this is an error because it's extremely unlikely a 6 year old would be able to sign up for a website in the first place, and then place an order. Aditionnally, any age below 18, as 18 years old is usually the minimum age to purchase on websites as making purchases involves entering into a contract, hence the age restriction. Another abnormal value could be over the age of 80, whilst it may be entirely possible someone over the age of 85 made a purchase, the likelhihood is statistically low. The older you get after a certain age, the less likely you are to make an online purchase. Here's a graph showing the distributio nof digital buyers in the United States as of February 2020. https://www.statista.com/statistics/469184/us-digital-buyer-share-age-group/In our dataset the range In our dataset, the age range is 18-78, which seems like a normal age range.

Date:
The date column is in the correct data type which is "date". Running the filter once again we can see the months from January to December in 2022, no abnormalities can be seen here.

Status:
Running the filter, we can see "Cancelled", "Delivered", "Refunded" and "Returned", nothing abnormal to be seen here. It will be worth checking in the data dictionary, relevant documentation or with the data engineers/relevant contact person whether orders with delivery on the way need to be included too. 

Channel:
Running the filter, we can see the list of channels, nothing abnormal noted here.

SKU:
Running the filter, we can see the SKU ends with the size of the item such as XXL as below. This is something to keep in mind. If we run across a SKU without a size at the end, this may need to be corrected. 

Category and size:
Running the filter, we can see no abnormalities in these columns.

Quantity:
Running the filter, we can see numeric values and also text values, such as "1" and "One", "2" and "Two". We will utilise the same process as before and run the find and replace function to replace the text values with numeric values. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/f07b7fbc-2994-4ff1-bbce-6fa6badbe187)
Before 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/8a813941-1c97-4dce-90df-11daabe1ece2)
After running find and replace

Currency:
Running the filter again, we can see "INR" (Indian Rupees) is the only text value used throughout the column. Since we know our store is in India and accepts payments in INR, this column seems like a waste of space and could be removed, howver, it's important to consult with the relevant stakeholders before doing so. In our analysis we'll leave the column as is. 

Amount:
Running the filter again, we can see no abnormal values, no values seem very low or very high nor look like they wouldn't fall within the normal range. 

Ship City, Ship State and Ship Postal Code:
Running filters once again and scanning, we cannot see any abnormalities here. All states are correct names of Indian states. 

Ship Country:
This is another column which could be deleted to clear space, since we already know that the data is looking at national orders in India only and not international orders.

So here we conclude our data cleaning phase. We will now move onto data processing

## Data Processing
Here we'll be processing such as calculations, to help us in our analysis further. As an example, we can create age brackets, to help simplify our analysis. We can create groups such as "Young adults", "Adults" and "Seniors". Young adults includes the ages 18 to 25. We have chosen 25 because that is when the brain reaches or almost reaches full devleopment and maturation. From 25 to 60 will be "Adults", we can name it "fully developed adults", but for simplicity lets keep it adults. Then 60+ will be "seniors. Let's call this column "age group" and use the following formula. 
=IF(F2<=25,"Young Adult",IF(F2<60,"Adult",IF(F2>=60,"Seniors")))
This formula tells excel to output "Young Adult" if the age value is equal to or below 25, output "Adult" if the age value is below 60 and to output "Seniors" if the age value is above 60. The values have been checked by scanning over the values in the age column and age group column to see if the ages are falling within the correct age bracket. 
Below is the result of our formula. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/135be8ce-96f4-45a4-9442-88667d3538df)


Another thing we can do is, we can extract the Month from the Date column, so we can analyse based on months, as this was one of the questions we needed to answer. If we convert the dataset into a table and insert a slicer, the filtering will be by inddividual dates and not months. To be able to filter by months, we'll need to extract the month from the date column into another column. To do that we will use the TEXT function, which is used to convert numbers to text. We will use the formula below.
=TEXT(F2,"mmm")
This formula instructs excel to to extract the month from the cell F2 into a short output of the month name. Using "mmm" will give you Dec and using "mmmm" will give you December. Below is the result of our formula:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/f424bef8-867b-48b2-b742-1d384cef0809)

One thing we can also do is, paste the Age Group and Month column as values. This way you remove the formulas from the sheet and improve speed. The formula's should be documented on a separate document so you have a written account of all the steps and changes you have made and you can reverse any errors. 

## Data Analysis
Let's start by creating a pivot table. Pivot tables are frequently used as they allow large datasets to be summarised quickly and easily. To create a pivot table, go to the insert tab and click pivot table, select your data range, click "add this to data model" (more on this in a bit) and click OK. We'll now utilise our PivotTable fields to create the charts we need to address the questions. 

1. Compare the monthly sales and orders using a single chart
2. Which month had the highest sales and count of orders?

Here we'll drag our month, amount and order id fields in the appropriate areas and turn off the grand totals. Here's how things are looking like so far. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/6a35afa1-fb7c-4fce-9a61-cdcc26f1285e)

We can see the amount of sales per month and the number of order Id's per month, but this does not equate to the number of unique orders per month. Due to the structure of our data, instead of Count, we have to use count distinct, which will only include an order ID once in the count. This is why we selected the "add this to data model" option, so we get the option to use count distinct. Below are the results after running count distinct. For January, the difference is more than 200, this is why have to be careful and make sure we're using the correct count function.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/12460746-d82f-4d63-bb44-89da9d263775)

Now we'll create a chart using the PivotChart function. Since we have two measures, with the count of order ID's in the thousands and the sum of amounts into the millions, we'll need to create a dual axis. We'll also do our formatting and explain why we chose to do certain formatting steps. Heres's what our final chart looks like:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/673797ca-db61-4f90-97e4-4f3df1a7fd5f)


- Removed grid lines to improve clarity and decluttering
- Formatted the Y axis for Sales and used the Format Code 0.00,, "M", this is to remove lengthy numbers and make the values easier to read, whilst decluttering the chart.
- Gave the chart a title so the read knows what information the chart is displaying.

3. Who generated the most sales, men or women?

Here we can utilise a couple of different charts, we can use a bar chart as before, with horizontal or vertical bars. Or, we can use a pie chart. Generally, pie charts are frowned upon and not considered best practice, as it can be difficult to intepret the values of the slices in comparison to other slices of the pie when you've got multiple thin slices. However, to provide the audience with a quick, general sense of the part to whole relationship of your data, where you don't have many precise slices, pie charts a good option. Since we only have men and women we are comparing, we'll utilise a pie chart. Below is our final chart. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/d934d65b-db1b-4e22-8eea-a71c9a5ea30a)

4. What are the different statuses of orders?

Here we'll utilise a horizontal bar chart, we can also utilise a pie chart, however, the difference in some of the statuses are 1%, which will give us thin slices cluttered together, a bar chart will separate these out in a easy to interpret manner. Since we want to see the percent of grand total, we have to go to valaue field settings and change "choose values as" to % of grand total. Below is our final chart.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/388c9327-1121-433f-b07b-3b435de60482)

5. Which are the top 10 states contributing most to sales?

Here we'll utilise a horizontal bar chart again. It's absolutely fine to use the same type of chart multiple times in a dashboard, as long as you're getting the information across clearly with minimal cognitive load. Horizontal bar charts are one of the best charts when comparing multiple data categories. A few reasons include, the bars are proportional to the values they represent, so the reader can get an idea of whats happening simply by looking at the bar lengths and/or the colours of the bars without having to read much text. Category labels are easier to display before the bars and data labels after the bars. These are one of the most widely used charts for these reasons alone. 
Here's our chart below after formatting

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/90d8c50d-f9c7-4b76-9952-32cb76784985)

6. What is the relationship between age and gender based on number of purchases?

Here we're looking at contribution towards the total number of purchases, segmented by gender and age. We'll utilise a column chart to show the contribution towards sales by each gender in the young adult, adult and senior age groups. Below is our final chart after formatting:


![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/9410bc2a-caf5-4bd4-a005-2e7d647809ec)

7. Which channel is contributing to maximum sales?

Here we'll create another horizontal bar chart to compare the different channels on sales. Below is our final chart after formatting:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/edbe927d-b67d-4a7e-a5d0-2ad5e771f733)

   

Once we have created the charts we need, we'll now add slicers, we'l also use the report connections function to connect our slicers/filters with all of the charts.

Insights:
- There was an increase in sales, peaking in March, with a decline till June, followed by an increase in August and then an overall decline in sales till December. Why was there a increase tilL March? It may have been promotions run by the store, or it may be due to other factors such as festivals happening, March is a major month for festivities in India, this may explain the peak in March. 
- 

SCRIPT
- Very first thing you should do is, is create a separate folder and file for your cleaning, never edit the original file given to you, if anything goes wrong and you can't revert back that is an issue. Make sure you make a copy first and work on that. Different companies have different practices of handling datasets, be sure to confirm these beforehand. 
-  Data here for a store, what you want to do is have a look at any data documentation provided to you to get a better understanding of the data in the columns. So for example, the different categories there should be. You can go to data tab select filter and see if the cateogries match with the documentation, same with other columns such as channel. Documentation is usually a data dictionnary whci hcontains information of the data tpe, the format of the data, a description of the data in the column and examples of what data should look like.
- We can check to see if our index column is in the correct sequence


DASHBOARD
- Use sparing colours, follow gestalt principles of design, white space, use colors sparingly
