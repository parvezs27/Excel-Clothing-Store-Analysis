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

The Data Engineers for the store have provided us with the dataset for 2022 in the form of an Excel file, which we'll be using for our analysis. The dataset can be found here: [modern_traditional_data](/modern/).

We have been given the dataset and the questions we need to answer, however, a lot of the time in the real world this will not be the case. Data Analysts will be given a business problem and it will be upto us to decide which data we need, where to source the data from e.g. internally from within the company database or from an external source and which questions should be addressed to help solve the business problem. In this case, we haven't been given mock ups or example dashboards, however, the executives have mentioned that we're free to design the dashboard how we would like, as long as the information addresses the questions and is clearly and easily conveyed. 

In this project, we will begin with data cleaning, then move onto data processing and analysis, and finally, data visualisation.

## Data Checking
The very first thing we will do, is create a copy of our dataset. Never work on the original dataset and alter the data, if something goes wrong and is not able to be reversed, we've just corrupted our data and we're in trouble. We will also create a document, where we'll document this task and include details such as the starting and completion dates, the critical steps taken to complete the task, the primary formulas and functions used, any details of meetings related to the tasks and the issues we ran into and how we solved them. Whilst this may sound like too much, documenting your work is extremely important so you have a written account of your work which you can refer back to or share with the relevant stakeholders if required. The dataset and documentation will all be saved into a folder in a secure location and in an external location such as a secure encrypted external hard drive. 

We will now check over our data, this can be viewed as the analysis before the analysis. We have been given data by the engineers, who are highly educated and qualified professionals, however, as best practice, we have to make sure the data is appropriate for our task. 

Upon opening the dataset, we can see certain columns providing demographic data such as gender and age, as well as columns such as the ship city column providing geographic data. Additionally, we can also see columns which provide us with customer purchase information such as what channels are being used to make purchases, what categories are being purchased from, which sizes and the quantities and the price of each item. Finally, there are also ID columns such as customer ID and order ID, as well as an index, which can all be viewed as keys. These keys act as unique identifiers assigned to a particular piece of information such as customer ID or order ID, which can be used to connect tables with other tables in a database. In this dataset an index column provides a unique identifier for each row, where each row denotes the whole of a single order or a part of an order. This is an appropriate structure of the data, with each row representing the sale of each item and Order ID's separated on different rows, which allows us to analyse item sales easily. 

From this data, we can already see that we have the information to help us understand the stores customer base. Having demographic, geographic, behavioural and psychographic data can help with customer profiling and in gaining a deeper understanding of the customer. This information can then be used to drive business decisions such as marketing based decisions e.g. how to market to each segment of the customer base, how much to market and inventory based decisions e.g. which products should be stocked more or less.

Here's a snapshot of our data:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/4bcad4ff-da8d-4333-a7fe-e023a161876f)

*Image 1: Original Data Snapshot.*


Lets move onto data cleaning to make sure the data is in good shape before analysis.

## Data Cleaning and Preparation
Data cleaning is a **crucial** process, as we want our data to be in the best possible state, free from as much "rogue data" as possible. Rogue data being, incomplete, inaccurate, irrelevant, corrupt or incorrectly formatted data. Having accurate, complete, relevant and correctly formatted data will make sure our analysis is reliable and will make other tasks easier such as future analyses.

Lets start by checking for blanks, duplicates and inconsistencies within our data. To check for blanks/nulls in our dataset, we will highlight all the data by pressing Ctrl+A or double clicking the triangle on the left corner next to column A, then we'll utilise the go to special function by pressing F5, click "blanks", OK and Excel will begin scanning the dataset. We've received a "no cells were found" from Excel, which means there are no nulls in our dataset. 

If in the case we did get nulls, we would have to figure how to handle these nulls. Sometimes it's just a matter of looking at the data surrounding it and filling in the null. For example, you may have a customer who's purchased two items, these will be shown in two rows, each with an order ID and customer ID value. Lets say the order ID was missing for one of the rows, by looking at the other row and seeing that the order ID is the same, then it'll be clear that the customer ID will be the same too. 

In other cases, you may have to decide whether to use the mean, median, mode or another imputation method for handling null values. This entirely depends on the data and context, but generally, the mean is the most common method for imputation of numeric data. However, if there are outliers the mean can be heavily skewed in either direction. Where there are outliers, the median is a better option. The mode is more appropriate for categorical data and represents the most common category. These are not the only imputation methods, other methods include forward and backward fill for time series data and interpolation such as linear interpolation. It's important to liaise with stakeholders such as our managers and/or executives before using any of these methods, so we can make sure we are handling these values in alignment with preferred company practices. 

Moving along, we'll also have a look at our index column to see if the unique row identifiers are in sequential ascending order. To do this, we will use the formula: 

IF(OR((A2+1=A3),(A2-1=A1)),"Sequential","Not Sequential")

Here we're asking Excel to output "Sequential" if a cell plus 1 equals the value of the cell below it. If this condition is not met, Excel will output "Not Sequential". After running the formula, we will go to Data and add a filter to the column, so we can see the distinct values in the column. Here we can only see "Sequential", meaning that the values of the column are in ascending sequential order. If there was a "Not Sequential" shown, we would use the filter to find where this occurred and correct the issue. It's important we correct any errors with a key column as these key columns are used to connect tables with one another. 


![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/95185f25-7e03-4046-a64b-89ac387b51d4)

*Image 2: Index Column check.*

We will now go column by column checking for any issues. 

## Data Cleaning

**Order ID and Customer ID:**
The Order ID column contains numeric characters in a particular format, with 3 numeric characters followed by a dash and 7 numeric characters, followed by a dash and 7 numeric characters again. Upon adding a filter and scanning through the distinct values in the filter, all the order ID's seem to follow the same formatting with no abnormalities sticking out. Similarly with the customer ID column, using the same process of running a filter and scanning through, no issues or abnormalities standout.

**Gender:**
Already on first glance, we can see that there's "Women", "Men" and "W", indicating that genders have been denoted with both the word and the first letter of the word for the gender. We want to denote using just one method, here we'll denote the genders using the words "Men" and "Women" and replace any "M" and "W" with the words. To do that, we will filter for "M" and "W" and run the find and replace function and replace these with the appropriate gender.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/c6c52777-20c4-42a7-956b-37677bd738ec)

*Image 3: Gender column before cleaning.*

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/a0f7f1e0-30fd-4c4e-915b-776d542e6eed)

*Image 4: Gender column after cleaning.*

**Age:**
Using the filter, we will check for any abnormal values in the age column. As an example, if the value "6" was found, we would know for certain that this is an abnormal value because it's extremely unlikely a 6 year old would be able to sign up for a website in the first place, and then place an order. 18 years of age is the minimum age to purchase on websites as one is entering into a contract. 

Another abnormal value could be over the age of 90, whilst it may be entirely possible for someone over the age of 90 to make a purchase, the likelihood is statistically low. The older you get after a certain age, the less likely you are to make an online purchase. [Here](https://www.statista.com/statistics/469184/us-digital-buyer-share-age-group/) is a graph showing the distribution of digital buyers in the United States as of February 2020, showcasing the decreasing number of buyers with age. In our dataset the age range is 18-78, which can be said is a normal range when comparing to the graph above.

**Date:**
The date column is in the correct data type which is "date". Running through the filter, we can see the months from January to December in 2022 with no abnormalities to be seen.

**Status:**
Using our filter, we can see "Cancelled", "Delivered", "Refunded" and "Returned", nothing abnormal to be seen here.

**Channel:**
Using our filter, we can see the list of channels, nothing abnormal noted here.

**SKU:**
Using our filter,, we can see the SKU ends with the size of the item such as XXL. This is something we should keep in mind. If we run across a SKU without a size at the end, this may need to be corrected. 

**Category and size:**
Using the filter, we can see no abnormalities in these columns.

**Quantity:**
Using the filter, we can see numeric values and also text values, such as "1" and "One", "2" and "Two". We will utilise the same process as we did previously with the gender column and run the find and replace function to replace the text values with numeric values. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/f07b7fbc-2994-4ff1-bbce-6fa6badbe187)

*Image 5: Quantity column before cleaning.*

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/8a813941-1c97-4dce-90df-11daabe1ece2)

*Image 6: Quantity column after cleaning.*

**Currency:**
Using the filter, we can see "INR" (Indian Rupees) is the only text value used throughout the column. Since we already know our store is in India and accepts payments in INR, this column seems like an unnecessary use of space and could be removed. However, it's important to consult with the relevant stakeholders before doing so. In our analysis we'll leave the column as is. 

**Amount:**
Using the filter, we can see no abnormal values. No values seem very low or very high nor look like they wouldn't fall within the normal range. It would be useful to have a list of the item prices which we can refer to and see the item price range. If a value was to fall outside this range, we know there would be an error somewhere. 

**Ship City, Ship State and Ship Postal Code:**
Using the filter, we cannot see any abnormalities in these columns.

**Ship Country:**
This is another column which could be deleted to clear space, since we already know that the data is looking at national orders in India only and not international orders.

## Data Preparation

We will now perform a couple of calculations to help us with answering the questions. 

Question 6 for example asks us to identify the relationship between age and gender based on the number of purchases. To simplify this process, we will create age brackets/groups being "Young adults", "Adults" and "Seniors". If we don't create these groups, we'll be looking at all the individual ages on a chart. On a bar chart for example, there will be a bar for each age, this will be way too many bars and extracting insight from here would be extremely difficult. 

The age group for Young adults will include individuals aged from 18 to 25. We have chosen 25 because 25 is the approximate age where the human brain reaches full development and maturation. The "Adult" group will include individuals aged from 25 to 60. The "seniors" group will include individuals aged 60+. Let's call this column "age group" and use the following formula. 

=IF(F2<=25,"Young Adult",IF(F2<60,"Adult",IF(F2>=60,"Seniors")))

This formula instructs excel to output "Young Adult" if the age value is equal to or below 25, to output "Adult" if the age value is below 60 and to output "Seniors" if the age value is above 60. We've done a quick scan through the age and age group columns to make sure that the ages are falling within the right age group.

Below is the result of our formula. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/135be8ce-96f4-45a4-9442-88667d3538df)

*Image 7: Creating age groups/brackets.*

Now we'll extract the Month from the Date column, so we can answer question 2 which asks us to identify the month with the highest sales and orders. If we were to convert the dataset into a table and insert a slicer, we will only be able to filter by individual dates and not months. To be able to filter by months, we'll need to extract the month from the date column into another column. To do that, we will use the TEXT function which is used to convert numbers to text. We will use the formula below.

=TEXT(F2,"mmm")

This formula instructs excel to extract the numeric value of the month from the cell F2 into text form. Using "mmm" will result in "Dec" and using "mmmm" will give you the full form as "December". Below is the result of our formula:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/f424bef8-867b-48b2-b742-1d384cef0809)

*Image 8: Extraction of month from Date column.*

One thing we can also do, is to paste the columns with formula's such as Age Group and Month as values. This way you remove the formulas from the sheet and improve processing speed. The formulas will be in our documentation for this project so we can safely remove them from the sheet if we desire to.

## Data Analysis
We will be using Pivot tables for our analysis. Pivot tables are frequently used in Excel based analyses as they allow large datasets to be summarised quickly and easily. To create a pivot table, we will go to the insert tab and click pivot table, select the data range, click "add this to data model" (more on this in a bit) and click OK. We'll now utilise our PivotTable fields to create the charts we need to address the questions. 

**1. Compare the monthly sales and orders using a single chart
2. Which month had the highest sales and count of orders?**

We'll start by dragging our month, amount and order ID fields in the appropriate rows and value fields and turn off the grand totals, as below.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/509944ae-ef88-408b-8cc7-f0e31591700f)

*Image 9: Creating Pivot Table for monthly data with count.*

We can see the amount of sales and the number of Order ID's per month which Excel has counted, however, this count of order ID's does not equate to the count of unique orders per month. Due to the structure of our data, Excel count's every time an Order ID is mentioned in the dataset, so if an order ID is mentioned 3 times, it will be counted as 3 different orders. 

Instead of count, we have to use count distinct which will only count each order ID once. This was why we selected the "add this to data model" option, which allows us to use the count distinct function. Below are the results after running the count distinct function. We can see the difference is more than 200 for the month of January, this is why we have to be careful and make sure we're using the correct count function.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/12460746-d82f-4d63-bb44-89da9d263775)

*Image 10: Creating Pivot Table for monthly data with count distinct.*

Now we'll create a single chart which visualises monthly sales and orders using the PivotChart function. Since we have two measures, with the count of order ID's in the thousands and the sum of amounts into the millions, we'll need to create a dual axis chart.

Here's what our final chart looks like after formatting:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/eff02cc0-3ce1-43a7-b217-e6cfee979846)

*Image 11: Column Chart of sales and orders by month.*

**3. Who generated the most sales, men or women?**

Here we can utilise a couple of different charts, we can use a bar chart as before, with horizontal or vertical bars. Or, we can use a pie chart. Generally, pie charts are frowned upon and not considered best practice, as it can be difficult to interpret and distinguish the difference between similar sized slices. However, to provide the audience with a quick general sense of the part to whole relationship of your data where you don't have many precise slices, pie charts are a good option. Since we only have men and women we are comparing, we'll utilise a pie chart. Below is our final chart. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/d934d65b-db1b-4e22-8eea-a71c9a5ea30a)

*Image 12: Pie Chart of Men vs Women based on revenue generated.*

**4. What are the different statuses of orders?**

For this question we will use a horizontal bar chart, we can also utilise a pie chart, however, the difference in some of the statuses are 1%, which will give us thin slices cluttered together, a bar chart will separate these out in a easy to interpret manner. Since we want to see the percent of the grand total, we have to go to value field settings and change "choose values as" to % of grand total. Below is our final chart.

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/322ae808-05b0-45fd-9b7d-8562ba24e3af)

*Image 13: Bar Chart of order status.*

**5. Which are the top 10 states contributing most to sales?**

Here we'll use a horizontal bar chart again. Horizontal bar charts are one of the best charts when comparing multiple data categories. One reason is that the bars are proportional to the values they represent, which gives a clear indication of what's happening almost instantly to the audience. Another reason is that labels are easier to display, these include category labels before the bars and data labels after the bars. These reasons alone make horizontal bar charts one of the most used charts in visualisation. 
Here's our chart below after doing our formatting:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/90d8c50d-f9c7-4b76-9952-32cb76784985)

*Image 14: Bar Chart of top 10 states by sales.*

**6. What is the relationship between age and gender based on number of purchases?**

Here we're looking at the contribution towards the total number of purchases, segmented by gender and age. We'll utilise a column chart to show the contribution towards sales by each gender in the young adult, adult and senior age groups. Below is our final chart after formatting:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/0f00967e-35b5-4498-9aaa-493f86cffa64)

*Image 15: Column Chart of orders segmented by age and gender.*

**7. Which channel is contributing to maximum sales?**

Here we'll create another horizontal bar chart to compare the sales generated by different sales channels. Below is our final chart after formatting:

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/edbe927d-b67d-4a7e-a5d0-2ad5e771f733)

*Image 16: Bar Chart of sales generated by sales channel.*
   
Now that the charts have been created, we'll arrange these charts onto one dashboard and add slicers. The "report connections" function will be used to connect our slicers with all of the charts. After doing our formatting, here's what our final dashboard looks like. The dashboard provides interactivity through slicers, allowing the end user to filter the data based on months, sales channel and category. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/3fd0de1f-d1a9-43cb-8d42-2d0ea6eb07e1)

*Image 17: Annual Sales Report Dashboard 2022.*

## Insights

Lets answer our questions one by one and look into the insights.

**1. Compare the sales and orders using a single chart
2. Which month had the highest sales and count of orders?**

The highest amount of sales and orders occurred in March, with the lowest occurring in November to December. Orders and sales generally seem to be correlated, with orders increasing as sales increase and decreasing as sales decrease. There's a continuing rise in sales from January to March, which may be due to several reasons such as seasonal trends, sales/promotions run by the store and/or festive season. The month of March comprises of many nationwide festivals in India, which may explain why March generated the most sales and orders. There is a decline in sales and orders from April to June, with an increase in July and August, followed by a decline till December. 

It's important to understand as Analysts whether this is a yearly pattern which is expected, or if the pattern is different in 2022 compared to prior years. Why are sales rising from January to March and on a general decline from April to December? Is it increased competition? Is it product quality and negative reviews? Is it the weather? Is it due to socio-economic and/or political events/issues? All this is important to understand so we can understand what is happening in the business, why it could be happening and how we can help the business improve taking into account the internal and external factors. 

**3. Who generated the most sales, women or men?
6. What is the relationship between age and gender based on number of purchases?**

Overall across all age groups, 64% of total sales were generated by women, whilst the remaining 36% were generated by men. Drilling down into the age groups, we can see that women across all age groups generated twice as many orders as men did. Adults contributed the most to total orders, followed by young adults and lastly seniors. 

**4. What are the different statuses of orders?**

The vast majority of orders (92.6%) were delivered, with a very small number which were returned, cancelled or refunded. According to [Shopify](https://www.shopify.com/au/enterprise/blog/ecommerce-returns#:~:text=The%20average%20return%20rate%20for%20ecommerce%20is%20typically%2020%25%20to,product%20and%20its%20online%20description.) , the average return rate for Ecommerce businesses is 20-30%, and in comparison, the return rate for Modern Traditional Store was only 3.5%. This likely suggests that the store does a great a job in delivering exactly what the customer expects (quality, size), leading to fewer returns. 
**
5. Which are the top 10 states contributing most to sales?**

The top states such as Maharashtra, Karnataka and Uttar Pradesh all generated over $2M in sales, with Maharashtra in the lead. It's important to understand why the top states, are the top states. Is it because the clothing items are catered towards the demographic in these states? Is it because a promotion was run for customers in those states? As analysts, we'd do our best to study the intrinsic business factors and extrinsic factors (outside of the business) which may explain why the top states are at the top. 

**7. Which channels are contributing the most to sales?**

# Conclusions and Recommendations

Amazon, Myntra and Flipkart are contributing to sales by a much greater margin compared to other channels such as Ajio, Nalli and Meesho. Once again, as analysts we have to understand why is this happening. Is it because Amazon, Myntra and Flipkart are much bigger and established platforms? Do we have to market more on these platforms or the other platforms? Are the other channels growing rapidly and it's worth spending more marketing funds on them compared to the already established platforms?

All in all, from our analysis, the key things we have learned are:
- Women across all age groups purchase more than men.
- Maharashtra, Karnataka and Uttar Pradesh are the top 3 states by sales.
- Adults aged 25 to 59 purchase more than other age groups.
- Amazon, Flipkart and Myntra are the top 3 sales channels.
- Sales and orders continually rise from January to March.

From these insights, a recommendation we can provide to executives would be to market towards women, particularly those in the 25 to 59 age group located in Maharashtra, Karnataka and Uttar Pradesh, through the top sales channels like Amazon, Flipkart and Myntra, during months of increased sales from January to March. 

Strategies to increase sales during the lower sales months, among young adults and seniors and among the lower performing states can be brought into conversation. Discount offers, introduction of a new line of clothing catered towards young adults and the elderly and a friend referral offer, are some of the many strategies which can be utilised to increase sales in the lower performing domains. 

# Visualisation Practices

In this section I wanted to share some of the best practices I adopted for this project and the visualisations:

**Documenting Externally:**

This refers to keeping documentation outside of the dashboard and not embedding it within the dashboard. Whether it's Tableau, Excel or Power BI, many times you will see the dashboard documentation such as the data source embedded within the dashboard. This is not a best practice due to several reasons. 

Firstly, embedded documentation is not searchable. If we were looking for specific metrics or information, we'd have to click through each dashboard to find what we're looking for. Having the dashboard information and metrics in separate documentation makes it much easier to find the information, metric and dashboards you're after. Secondly, every time you need to edit embedded documentation, you will have to edit the dashboard and re-publish it, increasing the likelihood of encountering bugs or glitches. Finally, embedded documentation is not part of an optimal UI/UX experience for the end user. We want to try our best to de-clutter dashboards to reduce cognitive load on the end user, which is why it's best to keep documentation outside of dashboards/visualisations.

**Decluttering Visualisation** 

This refers to using design principles with an understanding of pre-attentive attributes, Gestalt    principles and principles of design. [This](https://womenwhocode.com/blog/talks-tech-42-principles-of-good-data-visualization) is a fantastic article explaining the design principles mentioned. However to explain briefly, attributes of a visualisation such as colours (number of colours, intensity) white space, shapes and proximity of objects are all important factors to an effective visualisation. Understanding how to use these correctly will ensure visualisations are clean, de-cluttered and reduce cognitive load on the end user.

In our dashboard, I have used colours sparingly with less intensity. Using too much colour with too much brightness can be over stimulating. Colours have been associated with genders across two of the charts, with orange referring to women and blue referring to men. If I were to add another chart involving gender with the same colour, the end user would not need to read the legend, they would already know which colours are associated with which gender. Alignment and whitespace, there is equal alignment between all tiles/charts and all charts are the same size, this is to maintain consistency, as anything that pops out and isn't consistent with everything else can be distracting. If one of the tiles was bigger than the other, this would stand out and act as a distraction. All gridlines have also been removed from the charts. Adopting a minimalist approach to visualisations is the way to go. 

To quickly add, before creating any visualisation it's important to keep in mind issues such as colour blindness, sensitivity to colours, difficulty reading small text and other visual deficiencies. These deficiencies are quite common, to give an idea, colour blindness affects 1 in 12 men and 1 in 200 women, it's very likely that throughout our careers as analysts we will have to cater our visualisations for individuals with these deficiencies.
