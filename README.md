# PowerBI-Projects.
Documentation 

 Group 1: Retail_Sales_Data.csv 

Dataset Descriptions: 
● Retail Sales: Retail transactions from multiple store branches with sales, 
payment, and satisfaction details. 
- 1199 Transactions
Transaction_ID,Date,Branch,Product_Category,Product_Name,Quantity,Unit_Price,Total_Sales(cedis),Payment_Method,Customer_Satisfaction
sample of 3:
T1000,07/01/2024,Kumasi,Electronics,Smartwatch,7,,,mobile money,4
T1001,28/06/2024,Kumasi,Groceries,Rice,3,173.42,520.26,Cash,6
T1002,04-07-24,Takoradi,Electronics,Charger,7,,,Mobile Money,6

Data Cleaning Steps
step - purpose
different date formats
empty transaction-id
missing values- empty 
check unique categories
inconsistent text case
mixed integers/string variables for satisfaction column
trim

9 blanks in QUANTITY column
1-10 --> no outlier ->> use average value to fill (5.6 -> 6)
Transform: replace null with 6

unit_price
12 N/A -> replaced with null
change type to decimal
- right-skewed (mean < median)
22 empty => transform - impute with median(307.30), because of outliers and high standard deviation.

total_sales
convert to decimals
 find median(1446.15) < find mean(1609.02),
skewed -> impute median for robustness to outliers

payment_method
Capitalize Each Word

customer_satisfaction
good: 23 rows
blank: 35 rows
count: 300
guess is: 1(worst)-6(best) : worst,worse,bad,good,better,best
so good should be 4, so impute
convert to whole number

WILL DO WHENVER WE ALL OUR ON CALL 
{
replace null with average rating for same item ( we can look for better way later)
- find avearge rating for each product_name

Per each unique product_name:
select product_name, customer_satisfaction 
	filter by product_name 	
		remove records with null in customer_satisfaction 
			return averageValue in customer_satisfaction 
gpr, merge left outer, addCustomColumn
if [Customer_Satisfaction] = null then [Grped.AverageRating] else [Customer_Satisfaction]
RESULT: customer_satisfaction_filled column

used graphs for item against customer rating
}

date to date_filled
For the Date Column, I changed the format using:
  = try Date.From([Date]) otherwise
  try Date.FromText([Date], [Culture = "en-GB"]) otherwise
  try Date.FromText([Date], [Culture = "en-US"]) otherwise
  null

 Missing or inconsistent ID patterns 
 Split by non-digit/digit, replaced blanks with “T”, filled down, and merged columns
 Maintained unique identifiers without disrupting data order


