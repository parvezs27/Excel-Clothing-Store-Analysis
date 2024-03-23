# Excel-Clothing-Store-Analysis
## Project Information
Employed as Data Analysts for Modern Traditional Clothing Store in India, who sell womens and mens clothing through various online channels such as Myntra, Ajio and Amazon. Business executives of Modern Traditional Clothing have requested us to create an annual sales report, with the purpose of understanding their customer base and how to grow their sales in 2023. the business is performing, to help them with business decisions. The executives have advised that they currently don't have any dashboards, and haven't exactly specified what they would like us to deliver. No specific guidance has been provided on how to approach the task, what metrics they would like to see or any examples they may have which they wish to recreate. As analysts, it is upto use to understand the business, the business situation, what the stakeholders will need to see and how to best showcase this keeping in mind the target audience. 

We have been given the dataset in the form of an excel file (link below). We will begin with data cleaning, then move onto processing, analysis and finally dashboard creation.

## Key points of this project
- Pie charts have been used, generally pie charts are frowned upon in data analysis, but since no thin slices we can do.
- Understand the audience, do they have vision isuses? Colorblindness? Red and green color blindness is the most common.

## Data Checking
This can be viewed as the analysis before the analysis. We have been given data but we have to make sure the data is appropriate for our task, will the data help us provide the executives with an understanding of their customer base and assist them with business decisions to grow their sales in 2023? Let's have a look. 
We can see columns providing demographic data such as gender and age. We also have a ship city column providing geographic information. We also have columns which provide us information on the customer purchases such as what channel they're using to purchase, what category their purchasing from, what sizes, the quantities and the amount of each item. There are also ID columns such as customer ID and order ID, as well as an index, these can be viewed as keys, which are unique identifiers assigned to a particular piece of information such as customers or orders. In this dataset an index column provides a unique identifier for each row, where each row denotes the whole of a single order or a part of an order. 
From this data, we can already see that we have the information to help us understand the stores customer base. From the data, we'll be able to gain insights such as, which gender and age group purchased/spent the most, what item did they purchase the most, which category they purchased the most from, which platform did they use the most to make these purchase, where they are located etc. Having demographic, geographic, behavioural and psychographic data can help in customer profiling and ultimately gain a deeper understanding of the customer. This information can then be used to drive business decisions such as which segment of the customer base to market to, which products should be stocked more, which sales channels need to be worked on/improved etc. We'll also be able to see which product and category overall were the most popular and made the most revenue, which city purchased/spent the most, which sales platform was the most popular etc. 
The data looks like it will be able to help us with the business task. If we're not able to get certain insights, we will note these down and mention these to the executives. Lets move onto data cleaning to make sure the data is in good shape before analysis.
All the cleaning processes will be showcased in a video. 

## Data Cleaning
Data cleaning is an **extremely crucial** process, as we want our data to be in the best possible state, free from as much "rogue data" as possible. Rogue data being, incomplete, inaccurate, irrelevant, corrupt or incorrectly formatted data. Having accurate, complete, relevant and correctly formatted data will make sure our analysis is reliable and will make other tasks easier such as future analyses or if the data needs to be viewed by someone else in the company who's authorised to do so. 

Lets start by checking for blanks, duplicates and inconsistencies within our data. To check for blanks/nulls in our dataset, we will highlight all the data by pressing ctrl+A or double clicking the triangle on the left corner next to A, then we'll utilise the go to special function by pressing F5, click blank, OK and Excel will begin scanning the dataset. We get a "no cells were found", so there are no blanks in our dataset. 

We will also check the index column to see if the unique row identifiers are in sequential ascending order. To do this, we will use the formula: IF(OR((A2+1=A3),(A2-1=A1)),"Sequential","Not Sequential")
Basically we are asking Excel to output "Sequential" if the cell above plus 1 equals the cell below, which is the output we want for all cells. If in the case, this condition is not met, Excel will output "Not Sequential". After running the formula, we will go to Data and add a filter to the column, so we can see the distinct values. Here we can only see "Sequential", meaning that the numbers of the column are in sequential order. If there was a "Not Sequential" shown, we would filter to find where this was and correct the issue as need be. 
![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/95185f25-7e03-4046-a64b-89ac387b51d4)

We will now go column by column checking for any issues, once again, we'll be looking out for any abnormal values, these could be an integer that's much lower or higher than the expected range, a repeat of value but with a spelling error etc.

Order ID: 
- Contains numeric characters for the order ID in a particular formatting, with 3 numeric characters followed by a dash and 7 numeric characters, followed by a dash and 7 numeric characters again. Upon adding a filter and scanning through the disctinct values in the filter, no issues stood out.
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
=IF(F4<=25,"Young Adult",IF(F4<60,"Adult",IF(F4>=60,"Seniors")))
This formula tells excel to output "Young Adult" if the age value is equal to or below 25, output "Adult" if the age value is below 60 and to output "Seniors" if the age value is above 60. The values have been checked by scanning over the values in the age column and age group column to see if the ages are falling within the correct age bracket. 
Below is the result of our formula. 

![image](https://github.com/parvezs27/Excel-Clothing-Store-Analysis/assets/107979122/135be8ce-96f4-45a4-9442-88667d3538df)






SCRIPT
- Very first thing you should do is, is create a separate folder and file for your cleaning, never edit the original file given to you, if anything goes wrong and you can't revert back that is an issue. Make sure you make a copy first and work on that. Different companies have different practices of handling datasets, be sure to confirm these beforehand. 
-  Data here for a store, what you want to do is have a look at any data documentation provided to you to get a better understanding of the data in the columns. So for example, the different categories there should be. You can go to data tab select filter and see if the cateogries match with the documentation, same with other columns such as channel. Documentation is usually a data dictionnary whci hcontains information of the data tpe, the format of the data, a description of the data in the column and examples of what data should look like.
- We can check to see if our index column is in the correct sequence


DASHBOARD
- Use sparing colours, follow gestalt principles of design, white space, use colors sparingly
