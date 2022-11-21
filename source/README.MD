# Information from the sales dept. 
-------------------------------
I have this Data-set from my workshop. I changed the information, so clients are safe :)

Here you can have a [quick view](What-we-have-in-the-source) of the Data-set final version (or download the .xlsx file). I will use it to build a model of DB, then I will make a DB and some visualisation

Also I will show you, [how I prepared](#It-was-different) the Data in the bottom :)



## What we have in the source.
-------------------------------

##### This is the main sheet, where we can find the basic info about the order and the client.
![source_screen_1](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss1.png)

##### This sheet is for the information about returned orders.
![source_screen_2](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss2.png)

##### We can find some info about products here
![source_screen_3](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss3.png)

##### Here is the info about the employees and the completed orders
![source_screen_4](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/ss4.png)




## It was different.
-------------------------------

1) [Original version](Original-version)
2) [Coloumn repairing](Coloumn-repairing)
  * [full_name](full_name)
  * [order_date, order_id](order_date,-order_id)
  * model_id
  * color_name
  * platform_name
  * phone_number
  * city_name
  * discount
  * delivery_price


### Original version
-------------------------------
When I started the work with the source file, it looked like this:

![past_source_1](https://github.com/victorjulyin/uncle_cat_shop/blob/main/pics/past_xlsx_1.png)

As you can see, the information is not structured well, also here are a lot of omissions.
We didn't need to keep these records very clean, because we needed more flexibility than purity :)


### Coloumn repairing
-------------------------------

There were problems at every coloumn, so I had to fix them.

##### full_name:
-------------------------------

At first I invented few names to fill blanks of this field and did it manually. 
Also I changed the table formatting.

![preparing_xlsx_1](вставить_ссылку)

##### order_date, order_id:
-------------------------------

I wanted the table to look natural. So I had to use some Python to reach it:

    d = [0,0,0,0,0,1,1,1]          # this var is to make the change of days random
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

This script:
1) produces the order_date and the order_id.
2) shuffles it by small parts, so the order execution sequence looks like in a real database.
3) prints it with tabulations, so I was able to copy/paste it to Google Sheets.

![idle_pic_1](вставить_скрин)