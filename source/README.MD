# Information from the sales dept. 

### Data-set from my workshop

I changed the information, so clients are safe :)

Here you can have a [quick view](#What-we-have-in-the-source) of the Data-set final version (or download the [.xlsx file](https://github.com/victorjulyin/uncle_cat_shop/blob/main/source/UncleCat_store_final.xlsx)). I will use it to build a model of DB, then I will make a DB and some visualisation

Also you can look, [how I prepared](#It-was-different) the Data in the bottom :)



## What we have in the source.

### This is the main sheet, where we can find the basic info about the order and the client.
![source_screen_1](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss1.png)

### This sheet is for the information about returned orders.
![source_screen_2](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss2.png)

### We can find some info about products here
![source_screen_3](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss3.png)

### Here is the info about the employees and the completed orders
![source_screen_4](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss4.png)




## It was different.

1. [Original version](#Original-version)
2. [Coloumn correction](#Coloumn-correction)
2.1 Coloumns that fixed manually:
  * full_name
  * city_name
  * delivery_price

2.2 Special coloumns:
  * [order_date, order_id](#order_date,-order_id)
  * [phone_number](#phone_number)

2.3 Coloumns made by the [similar way](#Other-coloumns):
  * model_id
  * color_name
  * platform_name
  * discount



  
  


## Original version

### It looked like this:

![past_source_1](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/past_xlsx_2.png)


As you can see, the information is not structured well, also here are a lot of omissions.
We didn't need to keep these records very clean, because we needed more flexibility than purity :)


## Coloumn correction
### * order_date, order_id:
I wanted the table to look natural. So I had to use some Python to reach it.

This script:
1) produces the random sum of days and the order_id.
2) shuffles it by small parts, so the order execution sequence looks like in a real database.
3) prints it with tabulations, so I was able to copy/paste it to Google Sheets.

    import random
    d = [0,0,0,0,0,1,1,1]          # this var is to make the days changing
    c = 0                          # this var shows "how many days passed"
    x1 = []                        # container 1
    x2 = []                        # container 2
    for i in range(100, 1000):     
        x1.append((i+1, c))        # filling the first container
        c += random.choices(d)[0]  # day passes or not?
        if len(x1) == 10:          # lets shuffle days and repeat
            random.shuffle(x1)
            x2.extend(x1)
            x1.clear()

    for (a, b) in x2:
        print(f'{a}\t{b}')          # printing with tabulations
    

#### Code result:
<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/idle_pic_1.png"></p>

#### Pasted into Google sheets:
<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/prep_xlsx_2_formula_order_date.png"></p>

#### Ready coloumns:
<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/prep_xlsx_3_order_date_fin.png"></p>

### * phone_number:
There were real phone numbers it this table, so I used two formulas in Google Sheets to transform this form of number 9154670185 (or 79154670185 sometimes) to 91546701

    =LEFT(H2;LEN(H2)-2)

    =IF(LEFT(H2,1)+0=7, RIGHT(H2,LEN(H2)-1), H2)



### * Other coloumns:
I used Python to make a random field with frequency that i needed.
Everything were the same instead of variable "b":

    import random
    b = ['brown', 'milk', 'grey', 'blue', 'brown', 'brown', 'milk', 'milk', 'milk', 'grey']
    for i in range(100):
        random.shuffle(b)
        
    for j in b:
        print(j)


Other options of variable "b":

    b = ['inst', 'fb', 'tg', 'c', 'inst', 'inst', 'fb', 'c', 'c', 'c']

    b = [0.02, 0.05, 0.10, 0, 0.02, 0.05, 0, 0, 0, 0]

    b = [1,2,2,2,2,4,4,5,5,5,6,6,6,7,8,8,8,10,11,11,12,13]




  