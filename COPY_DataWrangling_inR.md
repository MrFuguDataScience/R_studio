# R-Studio Data Wrangling and Cleaning:

# <font color=red>Mr Fugu Data Science</font>

# (◕‿◕✿)


# Purpose & Outcome:

+ Learn Different Techniques to manipulate your data

+ Extend your skills and learn something useful, and remember: `always, be leery of steely-eyed orange guys with weird hair and fake news.`

**Disclaimer**: always, evaluate your data and look at examples as just that; and NOT a savior to all your problems. These are tools to aid you NOT answer every concernt that comes up, because they are all different. 



```R
library(tidyverse)
library(knitr) # 

```

    ── [1mAttaching packages[22m ─────────────────────────────────────── tidyverse 1.3.0 ──
    
    [32m✔[39m [34mggplot2[39m 3.3.2     [32m✔[39m [34mpurrr  [39m 0.3.4
    [32m✔[39m [34mtibble [39m 3.0.1     [32m✔[39m [34mdplyr  [39m 1.0.0
    [32m✔[39m [34mtidyr  [39m 1.1.0     [32m✔[39m [34mstringr[39m 1.4.0
    [32m✔[39m [34mreadr  [39m 1.3.1     [32m✔[39m [34mforcats[39m 0.5.0
    
    ── [1mConflicts[22m ────────────────────────────────────────── tidyverse_conflicts() ──
    [31m✖[39m [34mdplyr[39m::[32mfilter()[39m masks [34mstats[39m::filter()
    [31m✖[39m [34mdplyr[39m::[32mlag()[39m    masks [34mstats[39m::lag()
    


# Sales Data With Removed Canceled Orders:
 


```R
sales_orders<-read.csv('SalesDataNoCancels.csv')

# head(sales_orders)

# head(subset(sales_orders$Country!='United Kingdom'))
# sales_wo_uk<-subset(sales_orders, Country!='United Kingdom')
```


```R
# One Way To Change to Date Format:
date_t_01<-sales_orders%>% mutate_at(vars(InvoiceDate), as.Date, format="%m/%d/%Y %H:%M")
head(date_t_01)
```


<table>
<caption>A data.frame: 6 × 10</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>CanceledQty</th><th scope=col>Matches</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>563614</td><td>23345</td><td> DOLLY GIRL BEAKER           </td><td>200</td><td>2011-08-18</td><td>1.08</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>2</th><td>568708</td><td>23391</td><td> I LOVE LONDON MINI BACKPACK </td><td>  4</td><td>2011-09-28</td><td>4.15</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>3</th><td>556917</td><td>22418</td><td>10 COLOUR SPACEBOY PEN       </td><td> 48</td><td>2011-06-15</td><td>0.85</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>4</th><td>543989</td><td>20973</td><td>12 PENCIL SMALL TUBE WOODLAND</td><td>384</td><td>2011-02-15</td><td>0.55</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>5</th><td>547659</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td> 12</td><td>2011-03-24</td><td>0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>6</th><td>556917</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td>240</td><td>2011-06-15</td><td>0.29</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
</tbody>
</table>




```R
# the UK dwarfs the data, that is why I remove it here:
sales_wo_uk<-subset(sales_orders, Country!='United Kingdom')
```

# Parsing the dates from the data for our examples today.


```R
# Taking the Date column and converting from char -> date/time
time_<-strptime(sales_wo_uk$InvoiceDate, "%m/%d/%Y %H:%M")

time_conversion<-as.POSIXct(time_) # convert object to class: date/time

dates_fix<-data.frame(
   date=time_conversion,
   hour=format(time_conversion, "%H"),
   day=format(time_conversion,"%d"),
   month=format(time_conversion,"%m"),
   year=format(time_conversion,"%Y"),
month_year=format(time_conversion,"%m/%Y"))



head(dates_fix)
```


<table>
<caption>A data.frame: 6 × 6</caption>
<thead>
	<tr><th></th><th scope=col>date</th><th scope=col>hour</th><th scope=col>day</th><th scope=col>month</th><th scope=col>year</th><th scope=col>month_year</th></tr>
	<tr><th></th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>2011-08-18 08:51:00</td><td>08</td><td>18</td><td>08</td><td>2011</td><td>08/2011</td></tr>
	<tr><th scope=row>2</th><td>2011-09-28 15:41:00</td><td>15</td><td>28</td><td>09</td><td>2011</td><td>09/2011</td></tr>
	<tr><th scope=row>3</th><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td></tr>
	<tr><th scope=row>4</th><td>2011-02-15 09:52:00</td><td>09</td><td>15</td><td>02</td><td>2011</td><td>02/2011</td></tr>
	<tr><th scope=row>5</th><td>2011-03-24 13:05:00</td><td>13</td><td>24</td><td>03</td><td>2011</td><td>03/2011</td></tr>
	<tr><th scope=row>6</th><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td></tr>
</tbody>
</table>




```R
# Month Name:
dates_fix$month_abbrv<-month.abb[as.numeric(dates_fix$month)]


# Day of Week Names
dates_fix$day_of_week<-strftime(dates_fix$date,'%A')
head(dates_fix)
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>date</th><th scope=col>hour</th><th scope=col>day</th><th scope=col>month</th><th scope=col>year</th><th scope=col>month_year</th><th scope=col>month_abbrv</th><th scope=col>day_of_week</th></tr>
	<tr><th></th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>2011-08-18 08:51:00</td><td>08</td><td>18</td><td>08</td><td>2011</td><td>08/2011</td><td>Aug</td><td>Thursday </td></tr>
	<tr><th scope=row>2</th><td>2011-09-28 15:41:00</td><td>15</td><td>28</td><td>09</td><td>2011</td><td>09/2011</td><td>Sep</td><td>Wednesday</td></tr>
	<tr><th scope=row>3</th><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td><td>Jun</td><td>Wednesday</td></tr>
	<tr><th scope=row>4</th><td>2011-02-15 09:52:00</td><td>09</td><td>15</td><td>02</td><td>2011</td><td>02/2011</td><td>Feb</td><td>Tuesday  </td></tr>
	<tr><th scope=row>5</th><td>2011-03-24 13:05:00</td><td>13</td><td>24</td><td>03</td><td>2011</td><td>03/2011</td><td>Mar</td><td>Thursday </td></tr>
	<tr><th scope=row>6</th><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td><td>Jun</td><td>Wednesday</td></tr>
</tbody>
</table>



# Create a new column of `Sales totals=Qty*Price`

+ This is just 1 way of doing this by the way


```R

sales_wo_uk$Sales_Tot<-sales_wo_uk$Quantity*sales_wo_uk$UnitPrice
head(sales_wo_uk)
```


<table>
<caption>A data.frame: 6 × 11</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>CanceledQty</th><th scope=col>Matches</th><th scope=col>Sales_Tot</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>563614</td><td>23345</td><td> DOLLY GIRL BEAKER           </td><td>200</td><td>8/18/2011 8:51 </td><td>1.08</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td>216.0</td></tr>
	<tr><th scope=row>2</th><td>568708</td><td>23391</td><td> I LOVE LONDON MINI BACKPACK </td><td>  4</td><td>9/28/2011 15:41</td><td>4.15</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td><td> 16.6</td></tr>
	<tr><th scope=row>3</th><td>556917</td><td>22418</td><td>10 COLOUR SPACEBOY PEN       </td><td> 48</td><td>6/15/2011 13:37</td><td>0.85</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td> 40.8</td></tr>
	<tr><th scope=row>4</th><td>543989</td><td>20973</td><td>12 PENCIL SMALL TUBE WOODLAND</td><td>384</td><td>2/15/2011 9:52 </td><td>0.55</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td>211.2</td></tr>
	<tr><th scope=row>5</th><td>547659</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td> 12</td><td>3/24/2011 13:05</td><td>0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td><td> 10.2</td></tr>
	<tr><th scope=row>6</th><td>556917</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td>240</td><td>6/15/2011 13:37</td><td>0.29</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td> 69.6</td></tr>
</tbody>
</table>



# If you had to combine two data frames:

+ There is `cbind`: which works columnwise, meaning it forms an abuttment.
    + Otherwise, you have `rbind`: which would just append to end of rows


```R
sales_orders_expanded<-cbind(sales_wo_uk,dates_fix)

head(sales_orders_expanded)
```


<table>
<caption>A data.frame: 6 × 19</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>CanceledQty</th><th scope=col>Matches</th><th scope=col>Sales_Tot</th><th scope=col>date</th><th scope=col>hour</th><th scope=col>day</th><th scope=col>month</th><th scope=col>year</th><th scope=col>month_year</th><th scope=col>month_abbrv</th><th scope=col>day_of_week</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>563614</td><td>23345</td><td> DOLLY GIRL BEAKER           </td><td>200</td><td>8/18/2011 8:51 </td><td>1.08</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td>216.0</td><td>2011-08-18 08:51:00</td><td>08</td><td>18</td><td>08</td><td>2011</td><td>08/2011</td><td>Aug</td><td>Thursday </td></tr>
	<tr><th scope=row>2</th><td>568708</td><td>23391</td><td> I LOVE LONDON MINI BACKPACK </td><td>  4</td><td>9/28/2011 15:41</td><td>4.15</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td><td> 16.6</td><td>2011-09-28 15:41:00</td><td>15</td><td>28</td><td>09</td><td>2011</td><td>09/2011</td><td>Sep</td><td>Wednesday</td></tr>
	<tr><th scope=row>3</th><td>556917</td><td>22418</td><td>10 COLOUR SPACEBOY PEN       </td><td> 48</td><td>6/15/2011 13:37</td><td>0.85</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td> 40.8</td><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td><td>Jun</td><td>Wednesday</td></tr>
	<tr><th scope=row>4</th><td>543989</td><td>20973</td><td>12 PENCIL SMALL TUBE WOODLAND</td><td>384</td><td>2/15/2011 9:52 </td><td>0.55</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td>211.2</td><td>2011-02-15 09:52:00</td><td>09</td><td>15</td><td>02</td><td>2011</td><td>02/2011</td><td>Feb</td><td>Tuesday  </td></tr>
	<tr><th scope=row>5</th><td>547659</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td> 12</td><td>3/24/2011 13:05</td><td>0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td><td> 10.2</td><td>2011-03-24 13:05:00</td><td>13</td><td>24</td><td>03</td><td>2011</td><td>03/2011</td><td>Mar</td><td>Thursday </td></tr>
	<tr><th scope=row>6</th><td>556917</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td>240</td><td>6/15/2011 13:37</td><td>0.29</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td><td> 69.6</td><td>2011-06-15 13:37:00</td><td>13</td><td>15</td><td>06</td><td>2011</td><td>06/2011</td><td>Jun</td><td>Wednesday</td></tr>
</tbody>
</table>



# Change Layout of Data :

For the first few examples, lets evaluate these data as `CustomerID`, `SalesTot`, `Monthyear`
to create a new table


```R
sub<-c('CustomerID','Sales_Tot','day_of_week')
head(sales_orders_expanded[sub])
```


<table>
<caption>A data.frame: 6 × 3</caption>
<thead>
	<tr><th></th><th scope=col>CustomerID</th><th scope=col>Sales_Tot</th><th scope=col>day_of_week</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>12415</td><td>216.0</td><td>Thursday </td></tr>
	<tr><th scope=row>2</th><td>12393</td><td> 16.6</td><td>Wednesday</td></tr>
	<tr><th scope=row>3</th><td>12415</td><td> 40.8</td><td>Wednesday</td></tr>
	<tr><th scope=row>4</th><td>12415</td><td>211.2</td><td>Tuesday  </td></tr>
	<tr><th scope=row>5</th><td>12434</td><td> 10.2</td><td>Thursday </td></tr>
	<tr><th scope=row>6</th><td>12415</td><td> 69.6</td><td>Wednesday</td></tr>
</tbody>
</table>



# *Reshape*: using `tidyr` which is found in `tidyverse`

`----------------------------------------------------`

# `Gather`: Wide to Long





```R
mean_<-c(60,50,40,30,10)
sd_<-c(2,1,3,2,4)
items<-c('a','a','b','c','d')
df_1<-data.frame(items,mean_,sd_)

df_1

gather(df_1,mean_,sd_,key='keys',value='vals')
```


<table>
<caption>A data.frame: 5 × 3</caption>
<thead>
	<tr><th scope=col>items</th><th scope=col>mean_</th><th scope=col>sd_</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>60</td><td>2</td></tr>
	<tr><td>a</td><td>50</td><td>1</td></tr>
	<tr><td>b</td><td>40</td><td>3</td></tr>
	<tr><td>c</td><td>30</td><td>2</td></tr>
	<tr><td>d</td><td>10</td><td>4</td></tr>
</tbody>
</table>




<table>
<caption>A data.frame: 10 × 3</caption>
<thead>
	<tr><th scope=col>items</th><th scope=col>keys</th><th scope=col>vals</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>mean_</td><td>60</td></tr>
	<tr><td>a</td><td>mean_</td><td>50</td></tr>
	<tr><td>b</td><td>mean_</td><td>40</td></tr>
	<tr><td>c</td><td>mean_</td><td>30</td></tr>
	<tr><td>d</td><td>mean_</td><td>10</td></tr>
	<tr><td>a</td><td>sd_  </td><td> 2</td></tr>
	<tr><td>a</td><td>sd_  </td><td> 1</td></tr>
	<tr><td>b</td><td>sd_  </td><td> 3</td></tr>
	<tr><td>c</td><td>sd_  </td><td> 2</td></tr>
	<tr><td>d</td><td>sd_  </td><td> 4</td></tr>
</tbody>
</table>



# `separate`: Make Long Data Wide

+ spliting 1 column into multiple columns


```R
# `separate`: Make Long Data Wide, spliting 1 column into multiple columns


# sub_<-c('Country','CustomerID','Sales_Tot','day_of_week')
# head(sales_orders_expanded[sub_])
long_to_wide<-separate(sales_orders,'InvoiceDate',c('month','day','Year','hour','min'))

head(long_to_wide)
```


<table>
<caption>A data.frame: 6 × 14</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>month</th><th scope=col>day</th><th scope=col>Year</th><th scope=col>hour</th><th scope=col>min</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>CanceledQty</th><th scope=col>Matches</th></tr>
	<tr><th></th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>563614</td><td>23345</td><td> DOLLY GIRL BEAKER           </td><td>200</td><td>8</td><td>18</td><td>2011</td><td>8 </td><td>51</td><td>1.08</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>2</th><td>568708</td><td>23391</td><td> I LOVE LONDON MINI BACKPACK </td><td>  4</td><td>9</td><td>28</td><td>2011</td><td>15</td><td>41</td><td>4.15</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>3</th><td>556917</td><td>22418</td><td>10 COLOUR SPACEBOY PEN       </td><td> 48</td><td>6</td><td>15</td><td>2011</td><td>13</td><td>37</td><td>0.85</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>4</th><td>543989</td><td>20973</td><td>12 PENCIL SMALL TUBE WOODLAND</td><td>384</td><td>2</td><td>15</td><td>2011</td><td>9 </td><td>52</td><td>0.55</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>5</th><td>547659</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td> 12</td><td>3</td><td>24</td><td>2011</td><td>13</td><td>05</td><td>0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><th scope=row>6</th><td>556917</td><td>20984</td><td>12 PENCILS TALL TUBE POSY    </td><td>240</td><td>6</td><td>15</td><td>2011</td><td>13</td><td>37</td><td>0.29</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
</tbody>
</table>



# `Unite`: make 2 variables into 1

+ creating a time of hour and minutes together

if you do not put a separator, by default you will have an underscore 


```R
long_to_wide %>% unite(Time,hour,min,sep=':')
```


<table>
<caption>A data.frame: 387255 × 13</caption>
<thead>
	<tr><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>month</th><th scope=col>day</th><th scope=col>Year</th><th scope=col>Time</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>CanceledQty</th><th scope=col>Matches</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>563614</td><td>23345</td><td> DOLLY GIRL BEAKER                </td><td>200</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 1.08</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>568708</td><td>23391</td><td> I LOVE LONDON MINI BACKPACK      </td><td>  4</td><td>9 </td><td>28</td><td>2011</td><td>15:41</td><td> 4.15</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>556917</td><td>22418</td><td>10 COLOUR SPACEBOY PEN            </td><td> 48</td><td>6 </td><td>15</td><td>2011</td><td>13:37</td><td> 0.85</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>543989</td><td>20973</td><td>12 PENCIL SMALL TUBE WOODLAND     </td><td>384</td><td>2 </td><td>15</td><td>2011</td><td>9:52 </td><td> 0.55</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>547659</td><td>20984</td><td>12 PENCILS TALL TUBE POSY         </td><td> 12</td><td>3 </td><td>24</td><td>2011</td><td>13:05</td><td> 0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>556917</td><td>20984</td><td>12 PENCILS TALL TUBE POSY         </td><td>240</td><td>6 </td><td>15</td><td>2011</td><td>13:37</td><td> 0.29</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>547659</td><td>20983</td><td>12 PENCILS TALL TUBE RED RETROSPOT</td><td> 12</td><td>3 </td><td>24</td><td>2011</td><td>13:05</td><td> 0.85</td><td>12434</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>553546</td><td>23253</td><td>16 PIECE CUTLERY SET PANTRY DESIGN</td><td> 24</td><td>5 </td><td>17</td><td>2011</td><td>15:42</td><td>12.50</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>537676</td><td>22567</td><td>20 DOLLY PEGS RETROSPOT           </td><td> 24</td><td>12</td><td>8 </td><td>2010</td><td>9:53 </td><td> 1.25</td><td>12386</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>540700</td><td>22244</td><td>3 HOOK HANGER MAGIC GARDEN        </td><td> 12</td><td>1 </td><td>11</td><td>2011</td><td>9:47 </td><td> 1.95</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>556917</td><td>22150</td><td>3 STRIPEY MICE FELTCRAFT          </td><td>120</td><td>6 </td><td>15</td><td>2011</td><td>13:37</td><td> 1.65</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>563614</td><td>22150</td><td>3 STRIPEY MICE FELTCRAFT          </td><td> 80</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 1.65</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>545475</td><td>22839</td><td>3 TIER CAKE TIN GREEN AND CREAM   </td><td> 32</td><td>3 </td><td>3 </td><td>2011</td><td>10:59</td><td>12.75</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>545475</td><td>22838</td><td>3 TIER CAKE TIN RED AND CREAM     </td><td> 20</td><td>3 </td><td>3 </td><td>2011</td><td>10:59</td><td>14.95</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>554037</td><td>22838</td><td>3 TIER CAKE TIN RED AND CREAM     </td><td> 28</td><td>5 </td><td>20</td><td>2011</td><td>14:13</td><td>14.95</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>563614</td><td>22950</td><td>36 DOILIES VINTAGE CHRISTMAS      </td><td>288</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 1.25</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>556917</td><td>20979</td><td>36 PENCILS TUBE RED RETROSPOT     </td><td>128</td><td>6 </td><td>15</td><td>2011</td><td>13:37</td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>563614</td><td>20979</td><td>36 PENCILS TUBE RED RETROSPOT     </td><td>128</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>569650</td><td>20979</td><td>36 PENCILS TUBE RED RETROSPOT     </td><td>128</td><td>10</td><td>5 </td><td>2011</td><td>12:44</td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>569650</td><td>20978</td><td>36 PENCILS TUBE SKULLS            </td><td>128</td><td>10</td><td>5 </td><td>2011</td><td>12:44</td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>540267</td><td>22620</td><td>4 TRADITIONAL SPINNING TOPS       </td><td>160</td><td>1 </td><td>6 </td><td>2011</td><td>11:12</td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>545475</td><td>22620</td><td>4 TRADITIONAL SPINNING TOPS       </td><td>160</td><td>3 </td><td>3 </td><td>2011</td><td>10:59</td><td> 1.06</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>553546</td><td>22620</td><td>4 TRADITIONAL SPINNING TOPS       </td><td>320</td><td>5 </td><td>17</td><td>2011</td><td>15:42</td><td> 1.25</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>568708</td><td>22620</td><td>4 TRADITIONAL SPINNING TOPS       </td><td> 12</td><td>9 </td><td>28</td><td>2011</td><td>15:41</td><td> 1.45</td><td>12393</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>569650</td><td>22620</td><td>4 TRADITIONAL SPINNING TOPS       </td><td> 48</td><td>10</td><td>5 </td><td>2011</td><td>12:44</td><td> 1.45</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>563614</td><td>23353</td><td>6 GIFT TAGS VINTAGE CHRISTMAS     </td><td>216</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 0.72</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>540267</td><td>22077</td><td>6 RIBBONS RUSTIC CHARM            </td><td>144</td><td>1 </td><td>6 </td><td>2011</td><td>11:12</td><td> 1.45</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>563614</td><td>22952</td><td>60 CAKE CASES VINTAGE CHRISTMAS   </td><td>240</td><td>8 </td><td>18</td><td>2011</td><td>8:51 </td><td> 0.42</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>569650</td><td>23542</td><td>70'S ALPHABET WALL ART            </td><td>  6</td><td>10</td><td>5 </td><td>2011</td><td>12:44</td><td> 7.45</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>576394</td><td>84992</td><td>72 SWEETHEART FAIRY CAKE CASES    </td><td>120</td><td>11</td><td>15</td><td>2011</td><td>10:32</td><td> 0.42</td><td>12415</td><td>Australia</td><td>1</td><td>FALSE</td></tr>
	<tr><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td><td>⋮</td></tr>
	<tr><td>572215</td><td>22423</td><td>REGENCY CAKESTAND 3 TIER           </td><td> 3</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td>12.75</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23175</td><td>REGENCY MILK JUG PINK              </td><td> 4</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 3.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23174</td><td>REGENCY SUGAR BOWL GREEN           </td><td> 4</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 4.15</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23173</td><td>REGENCY TEAPOT ROSES               </td><td> 4</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 9.95</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23366</td><td>SET 12 COLOURING PENCILS DOILY     </td><td>16</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 0.65</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>580553</td><td>23366</td><td>SET 12 COLOURING PENCILS DOILY     </td><td>72</td><td>12</td><td>5 </td><td>2011</td><td>10:14</td><td> 0.65</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>22989</td><td>SET 2 PANTRY DESIGN TEA TOWELS     </td><td> 6</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 3.25</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>580553</td><td>23305</td><td>SET 4 PICNIC CUTLERY BLUEBERRY     </td><td>12</td><td>12</td><td>5 </td><td>2011</td><td>10:14</td><td> 1.95</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>580553</td><td>23304</td><td>SET 4 PICNIC CUTLERY CHERRY        </td><td>12</td><td>12</td><td>5 </td><td>2011</td><td>10:14</td><td> 1.95</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>580553</td><td>23303</td><td>SET 4 PICNIC CUTLERY FONDANT       </td><td>12</td><td>12</td><td>5 </td><td>2011</td><td>10:14</td><td> 1.95</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23328</td><td>SET 6 SCHOOL MILK BOTTLES IN CRATE </td><td>24</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 3.39</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>580553</td><td>23328</td><td>SET 6 SCHOOL MILK BOTTLES IN CRATE </td><td>24</td><td>12</td><td>5 </td><td>2011</td><td>10:14</td><td> 3.39</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23293</td><td>SET OF 12 FAIRY CAKE BAKING CASES  </td><td>32</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 0.83</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23295</td><td>SET OF 12 MINI LOAF BAKING CASES   </td><td>24</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 0.83</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>22720</td><td>SET OF 3 CAKE TINS PANTRY DESIGN   </td><td> 1</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 4.95</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23245</td><td>SET OF 3 REGENCY CAKE TINS         </td><td> 4</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 4.95</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>84987</td><td>SET OF 36 TEATIME PAPER DOILIES    </td><td> 3</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 1.45</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>22993</td><td>SET OF 4 PANTRY JELLY MOULDS       </td><td> 1</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 1.25</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>22734</td><td>SET OF 6 RIBBONS VINTAGE CHRISTMAS </td><td> 6</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 2.89</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23294</td><td>SET OF 6 SNACK LOAF BAKING CASES   </td><td>24</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 0.83</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>22722</td><td>SET OF 6 SPICE TINS PANTRY DESIGN  </td><td> 7</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 3.95</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>23296</td><td>SET OF 6 TEA TIME BAKING CASES     </td><td>32</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 1.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>21124</td><td>SET/10 BLUE POLKADOT PARTY CANDLES </td><td>48</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 1.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>21123</td><td>SET/10 IVORY POLKADOT PARTY CANDLES</td><td>48</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 1.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>21122</td><td>SET/10 PINK POLKADOT PARTY CANDLES </td><td>48</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 1.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>572215</td><td>21121</td><td>SET/10 RED POLKADOT PARTY CANDLES  </td><td>48</td><td>10</td><td>21</td><td>2011</td><td>12:52</td><td> 1.25</td><td>12646</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>47580</td><td>TEA TIME DES TEA COSY              </td><td> 3</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 2.55</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>37501</td><td>TEA TIME TEA SET IN GIFT BOX       </td><td> 5</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 6.95</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>37500</td><td>TEA TIME TEAPOT IN GIFT BOX        </td><td> 4</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 4.95</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
	<tr><td>550644</td><td>21067</td><td>VINTAGE RED TEATIME MUG            </td><td> 6</td><td>4 </td><td>19</td><td>2011</td><td>16:19</td><td> 1.25</td><td>12733</td><td>USA</td><td>1</td><td>FALSE</td></tr>
</tbody>
</table>



# `Seperate_rows`: Convert 1 column into more rows from an invidual cell



```R
shoe_types<-c('trail, street,hybrid','track,sandals','walking','high heels',
              -'pumps','boots')
arch_type<-c('high','low','flat','medium','extra crazy','who knows')
size_s<-c(9,10,11,12,13,7)

shoes_stuff<-data.frame(shoe_types,arch_type,size_s)
shoes_stuff
```


    Error in -"pumps": invalid argument to unary operator
    Traceback:




```R
shoes_stuff %>% separate_rows(shoe_types,sep=',')
```

#  `Spread`:  separates each cell into a column

Think of using a two columns: one as a key, other as a values. then you take the column that was a key and expand that into more columns based on unique row values. 


```R
ww<-shoes_stuff %>% separate_rows(shoe_types,sep=',')
ww%>% spread(shoe_types,size_s) 
```

# `Complete`: takes a set of cloumns and finds all combinations that are unique. *It will fill in NA values  when neccessary*.


```R
sub_w<-c('CustomerID','Sales_Tot','month_year')
a<-as.factor(sales_orders_expanded[sub_w]$month_year)
cc<-sales_orders_expanded[sub_w]
cc$date_col_asfactor<-a

complete(data = head(cc,10 ),date_col_asfactor)

# Notice that the datatypes 'classes' are not the same
```


```R
# read.csv('online_sales.csv')
```

# What is `Dplyr`: it is a package inside `tidyverse` allowing us to manipulate and transform our data

+ As an artifact you are able to write code that is readable for humans and cogent. 
+ There are 5 very common functions ("verbs") that you will use when using `dplyr`
    + `filter`
    + `select`
    + `arrange`
    + `mutate`
    + `summarise`
    


https://programminghistorian.org/en/lessons/data_wrangling_and_management_in_R

# Let's find the shoes in stock in a certain size range:

+ Using: `filter and select`

`filter`: works by row

`select`: columnwise


```R
shoes_long_<-shoes_stuff %>% separate_rows(shoe_types,sep=',')

shoes_by_size_range <- shoes_long_ %>%
  filter(size_s >9 & size_s <12) %>%
  select(shoe_types,arch_type,size_s)

shoes_by_size_range



```

# `Arrange`: will arrange rows by a specific column value


```R
# Going from descending order of shoes by size
shoes_long_ %>% arrange(desc(size_s))
```


```R
# Alt. Example with 2 variables:
head(date_t_01 %>% arrange(desc(Country),desc(InvoiceDate)))
```

# `Mutate`: Add a new variable to DF, think column


```R
head(date_t_01 %>% mutate(SalesTotsYay=Quantity*UnitPrice))
```

# `Summarize`: 

Creates a new dataframe that will have one or more rows for grouping, you are using a function to count, calculate the mean etc as a new column.

https://dplyr.tidyverse.org/reference/summarise.html


```R


ss<-shoes_long_   %>% 
  tibble::as_tibble() 

# count number of shoes based on size
ss %>%
  group_by(size_s) %>%
  summarise( n = n())

ss # print just the original data

# Group by shoe size and arch_type then count numbers available
ss %>%
  group_by(size_s,arch_type) %>%
  summarise( n = n())
```

# `Nest & Chop`: 

+ `Nest`: creates a list of column dataframes
    + There is a reverse of this called `unnest`
    
+ `Chop`: preserve the width of a DF, it is converting row lists into columns
    
https://tidyr.tidyverse.org/reference/chop.html


```R
# Originsl data:
ss
# Nest:
ss %>% nest(size_arch = c(shoe_types, arch_type))

# Chop:
ss %>% chop( c(shoe_types, arch_type))

```

# Alt Example:


```R
df <- tibble(x = c(1, 1, 1, 2, 2, 3), y = 1:6, z = 6:1)
# Note that we get one row of output for each unique combination of
# non-nested variables
df %>% nest(data = c(y, z))
df %>% chop(c(y, z))
df

# https://tidyr.tidyverse.org/reference/nest.html (this example came from here)
```

# Pivot from Wide to Long: `pivot_longer`



```R
#starting data: wide format
wide_shoes<-ww%>% spread(shoe_types,size_s) 
wide_shoes
```


```R
#convert to long data with pivot_longer:
wide_shoes %>% pivot_longer(cols=2:10, names_to = "Quarter", values_to = "Delay")
```

# Going in reverse: Long to Wide using `pivot_wider`


```R
# shoes_stuff %>% separate_rows(shoe_types,sep=',')
long_shoes<-wide_shoes %>% pivot_longer(cols=2:10, names_to = "Footwear",
                                        values_to = "Sizes")

# pivot_wider: convert long->wide
long_shoes%>% pivot_wider( names_from = Footwear, values_from = Sizes) 

```

`----------------------------`

# <font color=red>LIKE</font>, Share &

# <font color=red>SUB</font>scribe

# Citations & Help:

# <font size=6>◔̯◔</font>

`Cheat Sheets`

https://rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf?utm_campaign=Data%2BElixir&utm_medium=web&utm_source=Data_Elixir_19#:~:text=Tidy%20Data%20%2D%20A%20foundation%20for,works%20as%20intuitively%20with%20R.&text=tidyr%3A%3Agather(cases%2C%20%22,4)%20Gather%20columns%20into%20rows

https://github.com/rstudio/cheatsheets/blob/master/data-import.pdf 

https://rstudio.com/resources/cheatsheets/

`Good Examples and documentation`

https://bookdown.org/mikemahoney218/IDEAR/data-wrangling.html

https://rstudio-pubs-static.s3.amazonaws.com/221386_a6b7054b6536462fb3ba49e0341142e5.html

https://uc-r.github.io/tidyr

http://biostat.mc.vanderbilt.edu/wiki/pub/Main/ColeBeck/datestimes.pdf

https://medium.com/analytics-vidhya/advanced-data-wrangling-in-r-4-f98693b92851
