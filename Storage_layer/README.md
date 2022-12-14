# Creating Data Base on PostgreSQL

## Data architecture
(Нарисовать, как будет выглядеть в общем наша модель - слои)
Нарисуем в draw.io, но сначала нужно изучить табло сервер с вот этими штуками для безопасности

ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ



## Data Model
Подробнее рассказать, чего да как она у нас функционирует
(Есть картинка в папке data_model и файл с кодами для генерации таблиц)
НУЖНО ещё сделать файл с кодами для заполнения таблиц данными

ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ

<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/Storage_layer/Data_model/data_model1.png"></p>

Тут показать пример кода для создания таблицы и ссыль на файл с кодами



## SQL-queries to fill DB storage layer

### How I filled these tables

You can find the file with queries [here]()

If you want to know what problems I had and more about this process:
  1) [city](#table-city)
  2) 

ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ
ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ ДОПОЛНИТЬ

### Table "city"

<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/Storage_layer/pics/city_table3.png"></p>

#### Problems 

  1) Letter case
  2) Spaces
  3) Marks
  4) There was no info about base delivery price at the source (I decided to make it after the source creation). So I should insert this info into our DW now


#### 1-3) You can look at these problems here:
<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/Storage_layer/pics/city_table1.png"></p>


#### It was easy to solve it

Firstly, I deleted all spaces and made case low:

  UPDATE orders
  SET city_name = TRIM(LOWER(city_name))

After that I just found marks manually and corrected it:

  UPDATE orders
  SET city_name = 'зеленоград'
  WHERE city_name = 'зеленоглад';

  UPDATE orders
  SET city_name = 'москва'
  WHERE city_name = 'москаа';

<p align="center"><img  src="https://github.com/victorjulyin/uncle_cat_shop/blob/main/Storage_layer/pics/city_table2.png"></p>


#### 4) I decided to create a table with base delivery prices in xlsx and add it into a DW

I just found distinct cities and put random price

Result that I had in xlsx:

  |city_id | city_name	 | base_price |
  -------------------------------------
  |  101   | аксаково	   | 400        |
  |  102   | алексин	   | 300        |
  |  103   | ангарск	   | 400        |
  |  104   | арсеньев	   | 300        |
  |  105   | архангельск | 200        |
  |  ...   | ...         | ...        |


As usual, I just created SQL-queries for table filling:

  INSERT INTO u_dw.city(city_id, city_name, base_delivery_price) VALUES (101,'аксаково',400);
  INSERT INTO u_dw.city(city_id, city_name, base_delivery_price) VALUES (102,'алексин',300);
  INSERT INTO u_dw.city(city_id, city_name, base_delivery_price) VALUES (103,'ангарск',400);
  INSERT INTO u_dw.city(city_id, city_name, base_delivery_price) VALUES (104,'арсеньев',300);
  INSERT INTO u_dw.city(city_id, city_name, base_delivery_price) VALUES (105,'архангельск',200);
  ...



### Table "platform"








Какие папки нужно создать:
1) папка с sql-запросами,  которые будут вытаскивать инфу из сурс, чтобы потом с помощью них вставить эту инфу в созданные таблицы => пример получившейся таблицы
2) папка, в которой рассказывается про Модель данных (в ней же файл с sql-запросами для создания самих таблиц)



