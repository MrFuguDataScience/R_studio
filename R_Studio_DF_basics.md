# `Dataframe Manipulation Using: R-Studio`

# <font color= red>Mr Fugu Data Sceicne</font>

# (◕‿◕✿)

# Purpose & Outcome:

+ Subsetting

+ Adding Rows or Columns

+ Sorting & Filtering

+ Find Null Values, Duplicates

+ Use Arrange function and Mutate


```R
library(markdown)
library(knitr)
library(tidyverse)
```

    ── [1mAttaching packages[22m ─────────────────────────────────────── tidyverse 1.3.0 ──
    
    [32m✔[39m [34mggplot2[39m 3.3.2     [32m✔[39m [34mpurrr  [39m 0.3.4
    [32m✔[39m [34mtibble [39m 3.0.1     [32m✔[39m [34mdplyr  [39m 1.0.0
    [32m✔[39m [34mtidyr  [39m 1.1.0     [32m✔[39m [34mstringr[39m 1.4.0
    [32m✔[39m [34mreadr  [39m 1.3.1     [32m✔[39m [34mforcats[39m 0.5.0
    
    ── [1mConflicts[22m ────────────────────────────────────────── tidyverse_conflicts() ──
    [31m✖[39m [34mdplyr[39m::[32mfilter()[39m masks [34mstats[39m::filter()
    [31m✖[39m [34mdplyr[39m::[32mlag()[39m    masks [34mstats[39m::lag()
    



```R
fake_ppl<-read.csv('noIndx.csv')
head(fake_ppl)
```


<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5399-3484-4724-7187</td><td>gso@qiegan.sqe          </td><td>Donyell Ann</td><td>Ospina</td><td>5219459148</td></tr>
	<tr><th scope=row>2</th><td>1630-5261-6108-7631</td><td>xnji@gfruaxqnvm.fha     </td><td>Bishop     </td><td>Siyed </td><td>4164254716</td></tr>
	<tr><th scope=row>3</th><td>4435-3866-1076-3595</td><td>dvyco@tkzhsop.zxg       </td><td>Connor     </td><td>Powers</td><td>3627413915</td></tr>
	<tr><th scope=row>4</th><td>3489-7099-9906-8660</td><td>fy@uvfhplatmz.cam       </td><td>Kylie      </td><td>Her   </td><td>3562764561</td></tr>
	<tr><th scope=row>5</th><td>8631-4500-5666-1510</td><td>rztkvliou@dkeinhgysf.deo</td><td>Anthony    </td><td>Vo    </td><td>7345795348</td></tr>
	<tr><th scope=row>6</th><td>1459-9918-1722-7369</td><td>jofmezlbp@iw.evx        </td><td>Mutammam   </td><td>Mares </td><td>3247247289</td></tr>
</tbody>
</table>




```R
sales_data<-read.csv('online_sales.csv')
head(sales_data)
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td></tr>
</tbody>
</table>



# Slicing Dataframe:
+ `If we want to subset or manipulate our dataframe we need to think of it as 2 dimensions: dataframe[rows,columns].`


```R
typeof(fake_ppl[[2]])
typeof(fake_ppl$email)
typeof(fake_ppl[2])
class(fake_ppl)
typeof(fake_ppl)
class(fake_ppl)
```


'character'



'character'



'list'



'data.frame'



'list'



'data.frame'



```R
# one row and all columns:
fake_ppl[2,]
```


<table>
<caption>A data.frame: 1 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>2</th><td>1630-5261-6108-7631</td><td>xnji@gfruaxqnvm.fha</td><td>Bishop</td><td>Siyed</td><td>4164254716</td></tr>
</tbody>
</table>




```R
# take only 1 row and 2 specified columns:
fake_ppl[2,c('first_name',"last_name")]
```


<table>
<caption>A data.frame: 1 × 2</caption>
<thead>
	<tr><th></th><th scope=col>first_name</th><th scope=col>last_name</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>2</th><td>Bishop</td><td>Siyed</td></tr>
</tbody>
</table>




```R
# two ways to get credit_card:
head(fake_ppl[[1]])
head(fake_ppl$credit_card)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'5399-3484-4724-7187'</li><li>'1630-5261-6108-7631'</li><li>'4435-3866-1076-3595'</li><li>'3489-7099-9906-8660'</li><li>'8631-4500-5666-1510'</li><li>'1459-9918-1722-7369'</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'5399-3484-4724-7187'</li><li>'1630-5261-6108-7631'</li><li>'4435-3866-1076-3595'</li><li>'3489-7099-9906-8660'</li><li>'8631-4500-5666-1510'</li><li>'1459-9918-1722-7369'</li></ol>




```R
# exclude credit_card column:
head(subset(fake_ppl,select=-credit_card))
```


<table>
<caption>A data.frame: 6 × 4</caption>
<thead>
	<tr><th></th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>gso@qiegan.sqe          </td><td>Donyell Ann</td><td>Ospina</td><td>5219459148</td></tr>
	<tr><th scope=row>2</th><td>xnji@gfruaxqnvm.fha     </td><td>Bishop     </td><td>Siyed </td><td>4164254716</td></tr>
	<tr><th scope=row>3</th><td>dvyco@tkzhsop.zxg       </td><td>Connor     </td><td>Powers</td><td>3627413915</td></tr>
	<tr><th scope=row>4</th><td>fy@uvfhplatmz.cam       </td><td>Kylie      </td><td>Her   </td><td>3562764561</td></tr>
	<tr><th scope=row>5</th><td>rztkvliou@dkeinhgysf.deo</td><td>Anthony    </td><td>Vo    </td><td>7345795348</td></tr>
	<tr><th scope=row>6</th><td>jofmezlbp@iw.evx        </td><td>Mutammam   </td><td>Mares </td><td>3247247289</td></tr>
</tbody>
</table>




```R
# range of rows of first column:

fake_ppl[2:3,1]
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'1630-5261-6108-7631'</li><li>'4435-3866-1076-3595'</li></ol>




```R
# two ways to subset/slice the credit cards again: rows 4:7 of column 1

fake_ppl[4:7,1]
fake_ppl[[1]][4:7]
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'3489-7099-9906-8660'</li><li>'8631-4500-5666-1510'</li><li>'1459-9918-1722-7369'</li><li>'6736-8932-8180-5826'</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'3489-7099-9906-8660'</li><li>'8631-4500-5666-1510'</li><li>'1459-9918-1722-7369'</li><li>'6736-8932-8180-5826'</li></ol>



# Sort , Order , Rank:

+ `Sort`: returns the input as (ascending or descending) order

+ `Order`: the position 'index' of each input (ascending or descending) order

+ `Rank`: Will return the value of how it ranks from low to high or vice versa

https://statisticsglobe.com/sort-order-rank-r-function-example


```R
# Sort:

fun_list<- c(1,5,7,9,33,-4,-1)

sort(fun_list,decreasing = TRUE)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>33</li><li>9</li><li>7</li><li>5</li><li>1</li><li>-1</li><li>-4</li></ol>




```R
# Order:

order(fun_list,decreasing = TRUE)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>5</li><li>4</li><li>3</li><li>2</li><li>1</li><li>7</li><li>6</li></ol>




```R
# Rank: 

rank(fun_list)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>3</li><li>4</li><li>5</li><li>6</li><li>7</li><li>1</li><li>2</li></ol>



# Find `Null Values` & `Duplicates`:


```R
# Total NA values summed
sum(is.na(sales_data))

# Number of NA values by Column
colSums(is.na(sales_data))

# Print Out rows with NA: subset entries 5-10
unique(unlist (lapply (sales_data, function (x) which (is.na (x)))))[5:10]

#Print DF with NA Rows
head(sales_data[!!rowSums(is.na(sales_data)),])
```


135080



<style>
.dl-inline {width: auto; margin:0; padding: 0}
.dl-inline>dt, .dl-inline>dd {float: none; width: auto; display: inline-block}
.dl-inline>dt::after {content: ":\0020"; padding-right: .5ex}
.dl-inline>dt:not(:first-of-type) {padding-left: .5ex}
</style><dl class=dl-inline><dt>InvoiceNo</dt><dd>0</dd><dt>StockCode</dt><dd>0</dd><dt>Description</dt><dd>0</dd><dt>Quantity</dt><dd>0</dd><dt>InvoiceDate</dt><dd>0</dd><dt>UnitPrice</dt><dd>0</dd><dt>CustomerID</dt><dd>135080</dd><dt>Country</dt><dd>0</dd></dl>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1447</li><li>1448</li><li>1449</li><li>1450</li><li>1451</li><li>1452</li></ol>




<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>623</th><td>536414</td><td>22139</td><td>                               </td><td>56</td><td>12/1/2010 11:52</td><td>0.00</td><td>NA</td><td>United Kingdom</td></tr>
	<tr><th scope=row>1444</th><td>536544</td><td>21773</td><td>DECORATIVE ROSE BATHROOM BOTTLE</td><td> 1</td><td>12/1/2010 14:32</td><td>2.51</td><td>NA</td><td>United Kingdom</td></tr>
	<tr><th scope=row>1445</th><td>536544</td><td>21774</td><td>DECORATIVE CATS BATHROOM BOTTLE</td><td> 2</td><td>12/1/2010 14:32</td><td>2.51</td><td>NA</td><td>United Kingdom</td></tr>
	<tr><th scope=row>1446</th><td>536544</td><td>21786</td><td>POLKADOT RAIN HAT              </td><td> 4</td><td>12/1/2010 14:32</td><td>0.85</td><td>NA</td><td>United Kingdom</td></tr>
	<tr><th scope=row>1447</th><td>536544</td><td>21787</td><td>RAIN PONCHO RETROSPOT          </td><td> 2</td><td>12/1/2010 14:32</td><td>1.66</td><td>NA</td><td>United Kingdom</td></tr>
	<tr><th scope=row>1448</th><td>536544</td><td>21790</td><td>VINTAGE SNAP CARDS             </td><td> 9</td><td>12/1/2010 14:32</td><td>1.66</td><td>NA</td><td>United Kingdom</td></tr>
</tbody>
</table>




```R
# Take Care of NA values: REMOVE
no_naSales<-na.omit(sales_data)

#---------- Compare ------------
# Remove NA:
sum(is.na(no_naSales))

#original Data
sum(is.na(sales_data))
```


0



135080



```R
# Fill NA with other value: This is just 1 way of doing it

m<-sales_data %>% replace_na(list(CustomerID = "unknown"))
sum(is.na(m))
```


0



```R
# Find Duplicates:

head(sales_data[duplicated(sales_data),])
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>518</th><td>536409</td><td>21866</td><td>UNION JACK FLAG LUGGAGE TAG      </td><td>1</td><td>12/1/2010 11:45</td><td>1.25</td><td>17908</td><td>United Kingdom</td></tr>
	<tr><th scope=row>528</th><td>536409</td><td>22866</td><td>HAND WARMER SCOTTY DOG DESIGN    </td><td>1</td><td>12/1/2010 11:45</td><td>2.10</td><td>17908</td><td>United Kingdom</td></tr>
	<tr><th scope=row>538</th><td>536409</td><td>22900</td><td> SET 2 TEA TOWELS I LOVE LONDON  </td><td>1</td><td>12/1/2010 11:45</td><td>2.95</td><td>17908</td><td>United Kingdom</td></tr>
	<tr><th scope=row>540</th><td>536409</td><td>22111</td><td>SCOTTIE DOG HOT WATER BOTTLE     </td><td>1</td><td>12/1/2010 11:45</td><td>4.95</td><td>17908</td><td>United Kingdom</td></tr>
	<tr><th scope=row>556</th><td>536412</td><td>22327</td><td>ROUND SNACK BOXES SET OF 4 SKULLS</td><td>1</td><td>12/1/2010 11:49</td><td>2.95</td><td>17920</td><td>United Kingdom</td></tr>
	<tr><th scope=row>588</th><td>536412</td><td>22273</td><td>FELTCRAFT DOLL MOLLY             </td><td>1</td><td>12/1/2010 11:49</td><td>2.95</td><td>17920</td><td>United Kingdom</td></tr>
</tbody>
</table>




```R
# Remove Duplicates:

head(sales_data[!duplicated(sales_data),])
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td></tr>
</tbody>
</table>




```R
# Find Unique Values:

head(unique(sales_data))
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td></tr>
</tbody>
</table>




```R
# Same as Unique, but uses the dplyr method of distinct. If there is a duplicate row
# only the first is preserved

head(sales_data %>% distinct())
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td></tr>
</tbody>
</table>



# Filter: `find rows where some condition is TRUE`


```R
# Basic R:
head(filter(fake_ppl,first_name=='Anthony'))

# Dplyr Method:
head(fake_ppl %>% filter(first_name=='Anthony'))

# Can Also, Add other parameters:
head(fake_ppl %>% filter(first_name=='Anthony' & last_name=='Garcia'))


# Using filter to extract last names with specific starting character
head(filter(fake_ppl, grepl("Ga",last_name)))


# https://rstudio.com/wp-content/uploads/2016/09/RegExCheatsheet.pdf
```


<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>8631-4500-5666-1510</td><td>rztkvliou@dkeinhgysf.deo</td><td>Anthony</td><td>Vo      </td><td>7345795348</td></tr>
	<tr><th scope=row>2</th><td>1280-4584-5250-1133</td><td>axthrlcob@kdqvoabtw.nmg </td><td>Anthony</td><td>Henley  </td><td>6958349723</td></tr>
	<tr><th scope=row>3</th><td>6921-1083-1797-8702</td><td>xzgefkqlh@nhocyb.qwy    </td><td>Anthony</td><td>Hazelman</td><td>9315684987</td></tr>
	<tr><th scope=row>4</th><td>5725-6056-1230-2423</td><td>kj@tr.jdt               </td><td>Anthony</td><td>Garcia  </td><td>7244972846</td></tr>
	<tr><th scope=row>5</th><td>8170-8477-1042-3899</td><td>rexi@eitlpqv.pce        </td><td>Anthony</td><td>Green   </td><td>8362748419</td></tr>
	<tr><th scope=row>6</th><td>9895-2493-1052-5470</td><td>rm@fa.yka               </td><td>Anthony</td><td>Colorow </td><td>6813253162</td></tr>
</tbody>
</table>




<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>8631-4500-5666-1510</td><td>rztkvliou@dkeinhgysf.deo</td><td>Anthony</td><td>Vo      </td><td>7345795348</td></tr>
	<tr><th scope=row>2</th><td>1280-4584-5250-1133</td><td>axthrlcob@kdqvoabtw.nmg </td><td>Anthony</td><td>Henley  </td><td>6958349723</td></tr>
	<tr><th scope=row>3</th><td>6921-1083-1797-8702</td><td>xzgefkqlh@nhocyb.qwy    </td><td>Anthony</td><td>Hazelman</td><td>9315684987</td></tr>
	<tr><th scope=row>4</th><td>5725-6056-1230-2423</td><td>kj@tr.jdt               </td><td>Anthony</td><td>Garcia  </td><td>7244972846</td></tr>
	<tr><th scope=row>5</th><td>8170-8477-1042-3899</td><td>rexi@eitlpqv.pce        </td><td>Anthony</td><td>Green   </td><td>8362748419</td></tr>
	<tr><th scope=row>6</th><td>9895-2493-1052-5470</td><td>rm@fa.yka               </td><td>Anthony</td><td>Colorow </td><td>6813253162</td></tr>
</tbody>
</table>




<table>
<caption>A data.frame: 1 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>5725-6056-1230-2423</td><td>kj@tr.jdt</td><td>Anthony</td><td>Garcia</td><td>7244972846</td></tr>
</tbody>
</table>




<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>7332-5925-1286-6862</td><td>t@o.etk                 </td><td>Megana  </td><td>Garcia   </td><td>8961741498</td></tr>
	<tr><th scope=row>2</th><td>3580-5949-4055-7190</td><td>xbj@jvgxe.qhr           </td><td>Dylan   </td><td>Gashwazra</td><td>2657391284</td></tr>
	<tr><th scope=row>3</th><td>1320-8094-5183-6336</td><td>xedyh@ios.csh           </td><td>Noori   </td><td>Galbearth</td><td>8456758643</td></tr>
	<tr><th scope=row>4</th><td>9977-6665-6790-9118</td><td>fudyevgcrx@lsrxehqmn.rhv</td><td>Laquasea</td><td>Garcia   </td><td>4623196982</td></tr>
	<tr><th scope=row>5</th><td>9755-5822-3879-4403</td><td>ktsexfv@mxefpivrk.jeu   </td><td>Corey   </td><td>Gardner  </td><td>9538368157</td></tr>
	<tr><th scope=row>6</th><td>5725-6056-1230-2423</td><td>kj@tr.jdt               </td><td>Anthony </td><td>Garcia   </td><td>7244972846</td></tr>
</tbody>
</table>



# `Arrange` & `Mutate`:

+ `Arrange`: reorder or sort rows by column values

+ `Mutate`: adds new variables such as columns


```R
# Arrange:

head(sales_data  %>% arrange(Country))
```


<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536389</td><td>22941 </td><td>CHRISTMAS LIGHTS 10 REINDEER      </td><td> 6</td><td>12/1/2010 10:03</td><td>8.50</td><td>12431</td><td>Australia</td></tr>
	<tr><th scope=row>2</th><td>536389</td><td>21622 </td><td>VINTAGE UNION JACK CUSHION COVER  </td><td> 8</td><td>12/1/2010 10:03</td><td>4.95</td><td>12431</td><td>Australia</td></tr>
	<tr><th scope=row>3</th><td>536389</td><td>21791 </td><td>VINTAGE HEADS AND TAILS CARD GAME </td><td>12</td><td>12/1/2010 10:03</td><td>1.25</td><td>12431</td><td>Australia</td></tr>
	<tr><th scope=row>4</th><td>536389</td><td>35004C</td><td>SET OF 3 COLOURED  FLYING DUCKS   </td><td> 6</td><td>12/1/2010 10:03</td><td>5.45</td><td>12431</td><td>Australia</td></tr>
	<tr><th scope=row>5</th><td>536389</td><td>35004G</td><td>SET OF 3 GOLD FLYING DUCKS        </td><td> 4</td><td>12/1/2010 10:03</td><td>6.35</td><td>12431</td><td>Australia</td></tr>
	<tr><th scope=row>6</th><td>536389</td><td>85014B</td><td>RED RETROSPOT UMBRELLA            </td><td> 6</td><td>12/1/2010 10:03</td><td>5.95</td><td>12431</td><td>Australia</td></tr>
</tbody>
</table>




```R
# Mutate: adding a new column called Total_Price

head(sales_data  %>% mutate(Total_Price=Quantity*UnitPrice))
```


<table>
<caption>A data.frame: 6 × 9</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>Total_Price</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td><td>15.30</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td><td>22.00</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td><td>15.30</td></tr>
</tbody>
</table>



# `Cbind` & `Rbind`: combines by vector, matrix or dataframe

+ `Cbind`: columns

+ `Rbind`: rows

+ The number of rows [vector] will need to be the same length, if not then the shorter one will have repeating values to make up the difference in length

+ Matrices: they must be of same number of columns, or rows and if shorter there will be recyled values.
    + Matrices are restricted to a length of 2^31 rows

https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/cbind


```R
#cbind: add a column total_price

total_price <- c(sales_data$Quantity*sales_data$UnitPrice)

updated_sales<-cbind(sales_data,total_price)
# head(cbind(sales_data,total_price))
```


```R
# rbind: Add a row to end

vals<- c('1111-1111-1111-1111','MrFugu@funtimes.gov','Mr Fugu','DataScience','9999999999')

tail(rbind(fake_ppl,vals))
```


<table>
<caption>A data.frame: 6 × 5</caption>
<thead>
	<tr><th></th><th scope=col>credit_card</th><th scope=col>email</th><th scope=col>first_name</th><th scope=col>last_name</th><th scope=col>primary_phone_number</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>5822</th><td>4796-8595-9965-5748</td><td>knzos@jxlrmzk.xml     </td><td>Lavi           </td><td>Burd       </td><td>5266414287</td></tr>
	<tr><th scope=row>5823</th><td>1264-4045-4294-5090</td><td>swuljgompn@rgtxhba.jam</td><td>Leann          </td><td>Fang       </td><td>8398676395</td></tr>
	<tr><th scope=row>5824</th><td>6316-4730-8906-3877</td><td>xfsbe@kr.qbr          </td><td>Michael        </td><td>Song       </td><td>9867243254</td></tr>
	<tr><th scope=row>5825</th><td>8879-3013-4641-6431</td><td>bkmyozdafc@xnosg.pud  </td><td>Abraham Dejesus</td><td>Stevens    </td><td>7597526823</td></tr>
	<tr><th scope=row>5826</th><td>4360-6727-6740-5933</td><td>swkhc@vlme.dfx        </td><td>Angela         </td><td>al-Greiss  </td><td>7592516193</td></tr>
	<tr><th scope=row>5827</th><td>1111-1111-1111-1111</td><td>MrFugu@funtimes.gov   </td><td>Mr Fugu        </td><td>DataScience</td><td>9999999999</td></tr>
</tbody>
</table>



# Drop a Column:


```R
head(updated_sales)
head(subset(updated_sales,select = -c(total_price)))
```


<table>
<caption>A data.frame: 6 × 9</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th><th scope=col>total_price</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td><td>15.30</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td><td>22.00</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td><td>20.34</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td><td>15.30</td></tr>
</tbody>
</table>




<table>
<caption>A data.frame: 6 × 8</caption>
<thead>
	<tr><th></th><th scope=col>InvoiceNo</th><th scope=col>StockCode</th><th scope=col>Description</th><th scope=col>Quantity</th><th scope=col>InvoiceDate</th><th scope=col>UnitPrice</th><th scope=col>CustomerID</th><th scope=col>Country</th></tr>
	<tr><th></th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>1</th><td>536365</td><td>85123A</td><td>WHITE HANGING HEART T-LIGHT HOLDER </td><td>6</td><td>12/1/2010 8:26</td><td>2.55</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>2</th><td>536365</td><td>71053 </td><td>WHITE METAL LANTERN                </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>3</th><td>536365</td><td>84406B</td><td>CREAM CUPID HEARTS COAT HANGER     </td><td>8</td><td>12/1/2010 8:26</td><td>2.75</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>4</th><td>536365</td><td>84029G</td><td>KNITTED UNION FLAG HOT WATER BOTTLE</td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>5</th><td>536365</td><td>84029E</td><td>RED WOOLLY HOTTIE WHITE HEART.     </td><td>6</td><td>12/1/2010 8:26</td><td>3.39</td><td>17850</td><td>United Kingdom</td></tr>
	<tr><th scope=row>6</th><td>536365</td><td>22752 </td><td>SET 7 BABUSHKA NESTING BOXES       </td><td>2</td><td>12/1/2010 8:26</td><td>7.65</td><td>17850</td><td>United Kingdom</td></tr>
</tbody>
</table>



# Data.table



```R
total_by_country<-updated_sales[,c('Country','total_price')]
dt<-data.table(total_by_country)
head(dt[,list(Sum=sum(total_price)),by=Country])
```


<table>
<caption>A data.table: 6 × 2</caption>
<thead>
	<tr><th scope=col>Country</th><th scope=col>Sum</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>United Kingdom</td><td>8187806.36</td></tr>
	<tr><td>France        </td><td> 197403.90</td></tr>
	<tr><td>Australia     </td><td> 137077.27</td></tr>
	<tr><td>Netherlands   </td><td> 284661.54</td></tr>
	<tr><td>Germany       </td><td> 221698.21</td></tr>
	<tr><td>Norway        </td><td>  35163.46</td></tr>
</tbody>
</table>



# Writing to a file:
+ Write a file as a matrix
+ wirte a file as a vector

`write.csv(sub_meta, file="data/subset_meta.csv")`

or vector form: 

`write(glengths, file="data/genome_lengths.txt", ncolumns=1)`

Also, another option:

`write.table()`


`------------------------------------`

# <font color=red>Like</font>, Share &

# <font color=red>SUB</font>scribe

# Help & Citations:

# ◔̯◔

https://hbctraining.github.io/Intro-to-R/lessons/05_introR-data-wrangling2.html

https://stackoverflow.com/questions/25599139/identifying-rows-in-data-frame-with-only-na-values-in-r

https://www.datanovia.com/en/lessons/identify-and-remove-duplicate-data-in-r/#:~:text=The%20R%20function%20duplicated(),or%20data%20frame%20are%20duplicates.&text=!%20is%20a%20logical%20negation.%20!,don't%20want%20duplicate%20rows

https://stats.stackexchange.com/questions/8225/how-to-summarize-data-by-group-in-r

https://www.listendata.com/2016/10/r-data-table.html

https://stackoverflow.com/questions/24892529/dplyr-package-how-can-i-query-large-data-frame-using-like-xyz-sql-syntax
