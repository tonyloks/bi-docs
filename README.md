  # Основная техническая информация
хост:порт 77.232.130.241:8123\
login: admin\
password: 12345m678\
Схемы:
* default - пустая
* mp_db - основная
  
  # 1. Датасеты
Список датасетов:
1. [Выкупы](#Выкупы); 
1. [Основной датасет](#Основной_датасет);
1. [Остатки](#Остатки);
1. [Остатки размеры](#Остатки_размеры);
1. [План факт](#План_факт);
1. [Юнит экономика](#Юнит_экономика).
  # 2. Представления
Список представлений:
1. [mp_db.ads_stat_summary](#mp_db_ads_stat_summary);
1. [mp_db.articleadd](#mp_db_articleadd);
1. [mp_db.execute_plan](#mp_db_execute_plan);
1. [mp_db.kt_stat_summary](#mp_db_kt_stat_summary);
1. [mp_db.nmid_fullstat_renamed](#mp_db_nmid_fullstat_renamed);
1. [mp_db.order_current](#mp_db_order_current);
1. [mp_db.orders_stat_summary](#mp_db_orders_stat_summary);
1. [mp_db.paid_storage_summary](#mp_db_paid_storage_summary);
1. [mp_db.plan_fact_current](#mp_db_plan_fact_current);
1. [mp_db.sales_detail_report_summary](#mp_db_sales_detail_report_summary);
1. [mp_db.sales_stat_summary](#mp_db_sales_stat_summary);
1. [mp_db.stock_size](#mp_db_stock_size);
1. [mp_db.stocks_stat_new](#mp_db_stocks_stat_new);
1. [mp_db.unitka](#mp_db_unitka).
 # 3. Таблицы
Список таблиц:
1. [mp_db.ads_cost_history](#mp_db_ads_cost_history);
1. [mp_db.advert_stats](#mp_db_advert_stats);
1. [mp_db.cards_content](#mp_db_cards_content);
1. [mp_db.commissions](#mp_db_commissions);
1. [mp_db.cost_price](#mp_db_cost_price);
1. [mp_db.kt_stats](#mp_db_kt_stats);
1. [mp_db.orders_stat](#mp_db_orders_stat);
1. [mp_db.paid_storage](#mp_db_paid_storage);
1. [mp_db.product_plan](#mp_db_product_plan);
1. [mp_db.sales_detail_report_stat](#mp_db_sales_detail_report_stat);
1. [mp_db.sales_stat](#mp_db_sales_stat);
1. [mp_db.stocks_stat](#mp_db_stocks_stat).

    ## 1. Датасеты

### Выкупы
**Таблица / представление** - [mp_db.kt_stats](#mp_db_kt_stats)\
**Есть ли расчетные поля** - нет\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | id   | нет | Целое число / нет | [id](#mp_db_kt_stats) |
| 2 | nmID | нет | Целое число / нет | [nmID](#mp_db_kt_stats) |
| 3 | imtName   | нет | Строка / нет | [imtName](#mp_db_kt_stats) |
| 4 | vendorCode   | нет | Строка / нет | [vendorCode](#mp_db_kt_stats) |
| 5 | dt   | нет | дата и время / нет | [dt](#mp_db_kt_stats) |
| 6 | openCardCount   | нет | Целое число / нет | [openCardCount](#mp_db_kt_stats) |
| 7 | addToCartCount   | нет | Целое число / нет | [addToCartCount](#mp_db_kt_stats) |
| 8 | ordersCount   | нет | Целое число / нет | [ordersCount](#mp_db_kt_stats) |
| 9 | ordersSumRub   | нет | Дробное число / нет | [ordersSumRub](#mp_db_kt_stats) |
| 10 | buyoutsCount   | нет | Целое число / нет | [buyoutsCount](#mp_db_kt_stats) |
| 11 | buyoutsSumRub   | нет | Дробное число / нет | [buyoutsSumRub](#mp_db_kt_stats) |
| 12 | buyoutPercent   | нет | Дробное число / нет | [buyoutPercent](#mp_db_kt_stats) |
| 13 | addToCartConversion   | нет | Дробное число / нет | [addToCartConversion](#mp_db_kt_stats) |
| 14 | cartToOrderConversion   | нет | Дробное число / нет | [cartToOrderConversion](#mp_db_kt_stats) |


### Основной_датасет
**Таблица / представление** - [mp_db.nmid_fullstat_renamed](#mp_db_nmid_fullstat_renamed)\
**Есть ли расчетные поля** - да\
**Наличие параметров** - (scale_date - строка - день), (selected_measure - строка - количество)\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | Последняя выгруженная дата | ``` max([Дата] BEFORE FILTER BY [Дата]) ``` | дата / авто | нет |
| 2 | ДРР от продаж до спп   | ``` if [Выкупили на сумму, руб. (КТ)]!= 0 then [Расход, руб. (Р)] / [Выкупили на сумму, руб. (КТ)] else NULL end ``` | дробное число / авто | нет |
| 3 |  ДРР от заказов до спп  | ``` if [Заказали на сумму, руб. (КТ)] != 0     then [Расход, руб. (Р)] / [Заказали на сумму, руб. (КТ)] else    NULL end ```  | дробное число / авто | нет |
| 4 |  Артикул продавца  | ``` art.supplierArticle ```  | строка / нет | нет |
| 5 |  Продажи  | ``` if [selected_measure] = 'Количество'     then [Количество продаж, шт. (П)] ELSE [Цена со скидкой продавца, руб. (П)] end ```  | дробное число / авто | нет |
| 6 | Заказы   | ``` if [selected_measure] = 'Количество'    then [Количество заказов, шт. (З)] ELSE [Цена со скидкой продавца, руб. (З)] end ```  | дробное число / авто | нет |
| 7 |  CPC, руб.  | ``` IF [Клики (Р)] != 0    THEN [Расход, руб. (Р)]/[Клики (Р)] ELSE NULL END ```  | дробное число / авто | нет |
| 8 |  CR из перехода в заказ, %  | ``` if [Переходы в карточку (КТ)] != 0   then [Заказали товаров, шт. (КТ)]/ [Переходы в карточку (КТ)] else NULL end ```  | дробное число / авто | нет |
| 9 |  Продаж в день  | ``` sum([Количество продаж, шт. (П)]) / [Всего дней в датасете] ```  | дробное число / авто | нет |
| 10 | Заказов в день   | ``` sum([Заказали товаров, шт. (КТ)]) / [Всего дней в датасете] ```  | дробное число / авто | нет |
| 11 | Всего дней в датасете   | ``` ([Максимальная дата в датасете]-[Минимальная дата в датасете]) + 1 ```  | целое число / авто | нет |
| 12 |  Максимальная дата в датасете  | ``` if max([Дата]) is null then NULL ELSE max([Дата]) end  ```  | дата / авто | нет |
| 13 | Минимальная дата в датасете   | ``` if min([Дата]) is null then NULL ELSE min([Дата]) end ```  | дата / авто | нет |
| 14 |  ДРР рекламы | ``` if [Сумма заказов, руб. (Р)] != 0     then [Расход, руб. (Р)] / [Сумма заказов, руб. (Р)] else     NULL end ```  | дробное число / авто | нет |
| 15 |  ДРР аккаунта | ```  if [Заказали на сумму, руб. (КТ)] != 0     then [Расход, руб. (Р)] / [Заказали на сумму, руб. (КТ)] else     NULL end  ```  | дробное число / авто | нет |
| 16 | Карточка товара   | ``` URL('https://www.wildberries.ru/catalog/'+ str([ID карточки]) + '/detail.aspx', str([ID карточки])) ```  | разметка / нет | нет |
| 17 |  CR в заказ, % | ``` if [Переходы в карточку (КТ)] != 0     then [Заказали товаров, шт. (КТ)] / [Переходы в карточку (КТ)] else NULL end ```  | дробное число / авто | нет |
| 18 |  Ср. чек, руб. | ``` IF  [Цена со скидкой продавца, руб. (З)] != 0    THEN [Цена со скидкой продавца, руб. (З)]/[Количество продаж, шт. (П)] ELSE NULL END ```  | дробное число / авто | нет |
| 19 |  CPO, руб.  | ``` IF [Количество заказов, шт. (Р)] != 0     THEN [Расход, руб. (Р)]/[Количество заказов, шт. (Р)] ELSE NULL END  ```  | дробное число / авто | нет |
| 20 |  CTR, %  | ``` IF [Показы (Р)] != 0   THEN [Клики (Р)]/[Показы (Р)] ELSE NULL END ```  | дробное число / авто | нет |
| 21 |  Скалированная дата | ``` IF [scale_date] = 'День'     then [Дата] ELSEIF [scale_date] = 'Неделя'     then DATETRUNC([Дата],'week') ELSEIF [scale_date] = 'Месяц'     then DATETRUNC([Дата],'month') ELSEIF [scale_date] = 'Квартал'     then DATETRUNC([Дата],'quarter') ELSEIF [scale_date] = 'Год'     then DATETRUNC([Дата],'year') END  ```  | дата / нет | нет |
| 22 |   Выкуп, % | ``` if [Заказали товаров, шт. (КТ)] != 0     then sum([Выкупили товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) / sum([Заказали товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) else   NULL     end ```  | дробное число / авто | нет |
| 23 |   art.supplierArticle | нет | строка / нет | [art.supplierArticle](#mp_db_nmid_fullstat_renamed) |
| 24 |  ID карточки  | нет | целое число / нет | [ID карточки](#mp_db_nmid_fullstat_renamed) |
| 25 |  Дата  | нет | дата / нет | [Дата](#mp_db_nmid_fullstat_renamed) |
| 26 |  Название товара  | нет | строка / нет | [Название товара ](#mp_db_nmid_fullstat_renamed) |
| 27 |   Переходы в карточку (КТ) | нет | целое число / сумма | [Переходы в карточку (КТ)](#mp_db_nmid_fullstat_renamed) |
| 28 |   Положили в корзину (КТ) | нет | целое число / сумма | [Положили в корзину (КТ)](#mp_db_nmid_fullstat_renamed) |
| 29 |   Заказали товаров, шт. (КТ) | нет | целое число / сумма | [Заказали товаров, шт. (КТ)](#mp_db_nmid_fullstat_renamed) |
| 30 |   Заказали на сумму, руб. (КТ) | нет | целое число / сумма | [Заказали на сумму, руб. (КТ)](#mp_db_nmid_fullstat_renamed) |
| 31 |   Выкупили товаров, шт. (КТ) | нет | целое число / сумма | [Выкупили товаров, шт. (КТ)](#mp_db_nmid_fullstat_renamed) |
| 32 |   Выкупили на сумму, руб. (КТ) | нет | дробное число / сумма | [Выкупили на сумму, руб. (КТ)](#mp_db_nmid_fullstat_renamed) |
| 33 |   Количество заказов, шт. (З) | нет | целое число / сумма | [Количество заказов, шт. (З)](#mp_db_nmid_fullstat_renamed) |
| 34 |   Отмененный закаказов, шт. (З) | нет | целое число / сумма | [Отмененный закаказов, шт. (З)](#mp_db_nmid_fullstat_renamed) |
| 35 |   Выкупленных заказов, шт. (З) | нет | целое число / сумма | [Выкупленных заказов, шт. (З)](#mp_db_nmid_fullstat_renamed) |
| 36 |   Сумма заказов, руб. (З) | нет | дробное число / сумма | [Сумма заказов, руб. (З)](#mp_db_nmid_fullstat_renamed) |
| 37 |   Фактическая цена, руб. (З) | нет | дробное число / сумма | [Фактическая цена, руб. (З)](#mp_db_nmid_fullstat_renamed) |
| 38 |   Цена со скидкой продавца, руб. (З) | нет | дробное число / сумма | [Цена со скидкой продавца, руб. (З)](#mp_db_nmid_fullstat_renamed) |
| 39 |   Количество продаж, шт. (П) | нет | целое число / сумма | [Количество продаж, шт. (П)](#mp_db_nmid_fullstat_renamed) |
| 40 |   Сумма продаж, руб. (П) | нет | дробное число / сумма | [Сумма продаж, руб. (П)](#mp_db_nmid_fullstat_renamed) |
| 41 |   К перечислению, руб. (П) | нет | дробное число / сумма | [К перечислению, руб. (П)](#mp_db_nmid_fullstat_renamed) |
| 42 |   Фактическая цена, руб. (П) | нет | дробное число / сумма | [Фактическая цена, руб. (П)](#mp_db_nmid_fullstat_renamed) |
| 43 |   Цена со скидкой продавца, руб. (П) | нет | дробное число / сумма | [Цена со скидкой продавца, руб. (П)](#mp_db_nmid_fullstat_renamed) |
| 44 |   Показы (Р) | нет | целое число / сумма | [Показы (Р)](#mp_db_nmid_fullstat_renamed) |
| 45 |   Клики (Р) | нет | целое число / сумма | [Клики (Р)](#mp_db_nmid_fullstat_renamed) |
| 46 |   Расход, руб. (Р) | нет | дробное число / сумма | [Расход, руб. (Р)](#mp_db_nmid_fullstat_renamed) |
| 47 |   Положили в корзину, шт. (Р) | нет | целое число / сумма | [Положили в корзину, шт. (Р)](#mp_db_nmid_fullstat_renamed) |
| 48 |   Количество заказов, шт. (Р) | нет | целое число / сумма | [Количество заказов, шт. (Р)](#mp_db_nmid_fullstat_renamed) |
| 49 |   Кол-во заказанных товаров, шт. (Р) | нет | целое число / сумма | [Кол-во заказанных товаров, шт. (Р)](#mp_db_nmid_fullstat_renamed) |
| 50 |   Сумма заказов, руб. (Р) | нет | дробное число / сумма | [Сумма заказов, руб. (Р)](#mp_db_nmid_fullstat_renamed) |

### Остатки
**Таблица / представление** - [mp_db.stocks_stat_new](#mp_db_stocks_stat_new)\
**Есть ли расчетные поля** - да\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | if [Всего дней в датасете] > 0thensum([Продажи, шт.]) / [Всего дней в датасете]ELSE NULLend | ``` if [Всего дней в датасете] > 0 then sum([Продажи, шт.]) / [Всего дней в датасете] ELSE NULL end ``` | дробное число / авто | нет |
| 2 | Продажи Ср./День, шт.   | ``` if [Всего дней в датасете] > 0 then sum([Продажи, шт.]) / [Всего дней в датасете] ELSE NULL end ``` | дробное число / авто | нет |
| 3 |  На сколько дней хватит, продажи  | ``` if [Продажи Ср./День, шт.] > 0    then [Остатки, шт.] / [Продажи Ср./День, шт.] else NULL     ENd ```  | дробное число / авто | нет |
| 4 |  Дата последней продажи  | ``` max(max([Дата] INCLUDE [Дата],[nmId],[Склад]) EXCLUDE [Дата]) ```  | дата / нет | нет |
| 5 |  Дней без продаж, дни  | ``` date(now()) - [Дата последней продажи] ```  | целое число / авто | нет |
| 6 | ID карточки товара   | ```URL('https://www.wildberries.ru/catalog/'+ str([s.nmId]) + '/detail.aspx', str([s.nmId]))```  | разметка / нет | нет |
| 7 |  Ср. чек, руб.  | ```if [Продажи, шт.] > 0 then [Сумма продаж, руб.] / [Продажи, шт.] else NULL end  ```  | дробное число / авто | нет |
| 8 |  Стоимость остатка, руб.  | ``` [Ср. чек, руб.] * [Остатки, шт.] ```  | дробное число / авто | нет |
| 9 |  На сколько дней хватит, заказы  | ``` if [Заказов Ср./День, шт.] > 0    then [Остатки, шт.] / [Заказов Ср./День, шт.] else NULL   ENd ```  | дробное число / авто | нет |
| 10 | Заказов Ср./День, шт.   | ``` if [Всего дней в датасете] > 0 then sum([Общее Количество Заказов]) / [Всего дней в датасете] ELSE NULL end  ```  | дробное число / авто | нет |
| 11 | Сумма 1 дня простоя, руб.   | ``` if [Всего дней в датасете] > 0 then [Сумма продаж, руб.] / [Всего дней в датасете]  else NULL end  ```  | дробное число / авто | нет |
| 12 | Минимальная дата в датасете | ``` if min([Дата]) is null then NULL ELSE min([Дата]) end  ```  | дата / авто | нет |
| 13 | Максимальная дата в датасете | ``` if max([Дата]) is null then NULL ELSE max([Дата]) end  ```  | дата / авто | нет |
| 14 |  Всего дней в датасете | ```([Максимальная дата в датасете]-[Минимальная дата в датасете]) + 1```  | целое число / авто | нет |
| 15 |  Продажи, шт. | ```[Количество Продаж Всего] ```  | целое число / авто | нет |
| 16 | Сумма продаж, руб.   | ``` [Сумма Продаж По PriceWithDisc] ```  | дробное число / авто | нет |
| 17 |  Остатки, шт.| ```[Количество Остатков] ```  | дробное число / авто | нет |
| 18 |  Товаров по пути к клиенту, шт. | ```[Количество Товаров В Пути К Клиент] ```  | дробное число / авто | нет |
| 19 |  Артикул продавца  | ```[s.supplierArticle] ```  | строка / нет | нет |
| 20 | Дата  | нет  | дата / нет | [Дата](#mp_db_stocks_stat_new) |
| 21 | Склад | нет | строка / нет |[Склад](#mp_db_stocks_stat_new)|
| 22 | s.nmId | нет | целое число / нет | [s.nmId](#mp_db_stocks_stat_new) |
| 23 |  Количество Продаж Всего | нет | целое число / сумма | [Количество Продаж Всего](#mp_db_stocks_stat_new) |
| 24 |  Сумма Продаж По PriceWithDisc  | нет | дробное число / сумма | [Сумма Продаж По PriceWithDisc](#mp_db_stocks_stat_new) |
| 25 | Количество Остатков  | нет | целое число / среднее | [Количество Остатков](#mp_db_stocks_stat_new) |
| 26 | Количество Товаров В Пути К Клиент | нет | целое число / среднее | [Количество Товаров В Пути К Клиент](#mp_db_stocks_stat_new) |
| 27 | s.supplierArticle | нет | строка / нет | [s.supplierArticle](#mp_db_stocks_stat_new) |
| 28 | Общее Количество Заказов | нет | целое число / сумма | [Общее Количество Заказов](#mp_db_stocks_stat_new) |
| 29 | Общее Количество Продаж | нет | целое число / сумма | [Общее Количество Продаж](#mp_db_stocks_stat_new) |

### Остатки_размеры
**Таблица / представление** - [mp_db.stock_size](#mp_db_stock_size)\
**Есть ли расчетные поля** - нет\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | Карточка товара | ``` [nmId] ``` | строка / нет | нет |
| 2 | Ссылка | ``` URL('https://www.wildberries.ru/catalog/'+ str([Карточка товара]) + '/detail.aspx', str([Карточка товара])) ``` | разметка / нет | нет |
| 3 | warehouseName | нет  | строка / нет | [warehouseName](#mp_db_stock_size) |
| 4 | nmId | нет  | целое число / нет | [nmId](#mp_db_stock_size) |
| 5 | techSize | нет  | строка / нет | [techSize](#mp_db_stock_size) |
| 6 | quantity | нет  | целое число / нет | [quantity](#mp_db_stock_size) |

### План_факт
**Таблица / представление** - левое соединение 
[mp_db.plan_fact_current](#mp_db_plan_fact_current) - [mp_db.order_current](#mp_db_order_current)\
wb_sku = nmid_orders\
**Есть ли расчетные поля** - да\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | Месячный план | ``` [monthly_plan] ``` | дробное число / нет | нет |
| 2 | Количество заказов | ``` [sum(total_count_orders)] ``` | целое число / нет | нет |
| 3 | Карточка товара | ``` URL('https://www.wildberries.ru/catalog/'+ str([nmid_orders]) + '/detail.aspx', str([nmid_orders])) ```  | разметка / нет  | нет |
| 4 | Прогноз выполнения заказов | ``` ([Прогноз заказов]) / [Месячный план] ```  |  дробное число / нет  | нет |
| 5 | Выполнение плана | ``` [Количество заказов] / [Месячный план] ```  |  дробное число / нет | нет |
| 6 | Прогноз заказов | ``` [Количество заказов] + [Осталось дней] * [Среднее количество заказов ```  |  дробное число / нет  | нет |
| 7 | Осталось дней | ``` DAY((DATETRUNC(DATEADD(NOW(), "month"), "month") - 1)) - DAY(NOW()) ```  | целое число / нет | нет |
| 8 | Среднее количество заказов | ``` [Количество заказов] / [Дней с начала месяца] ```  |  дробное число / нет | нет |
| 9 | Дней с начала месяца| ``` DAY(NOW()) - DAY(DATETRUNC(NOW(), "month")) + 1 ```  | целое число / нет | нет |
| 10 | supplier_sku| нет |  строка / нет  | [supplier_sku](#mp_db_plan_fact_current) |
| 11 | wb_sku | нет | целое число / нет | [wb_sku](#mp_db_plan_fact_current) |
| 12 | month | нет | дата / нет | [month](#mp_db_plan_fact_current) |
| 13 | monthly_plan| нет | дата / авто | [monthly_plan](#mp_db_plan_fact_current) |
| 14 | nmid_orders| нет | целое число / нет | [nmid_orders](#mp_db_order_current) |
| 15 | sum(total_count_orders) | нет | целое число / нет | [sum(total_count_orders)](#mp_db_order_current) |

### Юнит_экономика
**Таблица / представление** - [mp_db.unitka](#mp_db_unitka)\
**Есть ли расчетные поля** - да\
**Наличие параметров** - (UnitType - строка - фактическая юнит экономика), (Nalog - Целое число - 1)\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | Комиссия ВБ | ```if [UnitType] = 'Общий отчет о продажах'    then SUM([sdrs.Комиссия ВБ]) ELSE SUM([sdrs.Комиссия ВБ]) / [sdrs.Количество] END ``` | дробное число / авто | нет |
| 2 | Логистика   | ``` if [UnitType] = 'Общий отчет о продажах'    then SUM([sdrs.Логистика]) ELSE SUM([sdrs.Логистика]) / SUM([sdrs.Количество]) END ``` | дробное число / авто | нет |
| 3 | Доля хранения  | ``` if [UnitType] = 'Общий отчет о продажах'    then AVG(SUM([Платное хранение]) /SUM([sdrs.Цена (со скидкой продавца, до СПП)])) ELSE AVG(SUM([Платное хранение]) / (SUM([sdrs.Цена (со скидкой продавца, до СПП)]) / SUM([sdrs.Количество]))) END ```  | дробное число / авто | нет |
| 4 | ДРР | ``` if [UnitType] = 'Общий отчет о продажах'    then AVG(SUM([Рекламные расходы]) / SUM([sdrs.Цена (со скидкой продавца, до СПП)])) ELSE AVG(SUM([Рекламные расходы]) / (SUM([sdrs.Цена (со скидкой продавца, до СПП)]) / SUM([sdrs.Количество]))) END ```  | дробное число / авто | нет |
| 5 | Себестоимость | ``` if [UnitType] = 'Общий отчет о продажах'    then AVG(IFNULL([cp.cost],0) * [sdrs.Количество]) ELSE AVG(IFNULL([cp.cost],0)) END ```  | дробное число / авто | нет |
| 6 | Доля логистики  | ``` AVG(IFNULL(SUM([sdrs.Логистика] INCLUDE [sdrs.Артикул ВБ]) / SUM([sdrs.Цена (со скидкой продавца, до СПП)] INCLUDE [sdrs.Артикул ВБ]), 0)) ```  | дробное число / авто | нет |
| 7 | Чистая прибыль  | ``` if [UnitType] = 'Общий отчет о продажах'    then AVG(SUM([sdrs.Цена (со скидкой продавца, до СПП)]) - SUM([Расходы])) ELSE AVG(((SUM([sdrs.Цена (со скидкой продавца, до СПП)])/ SUM([sdrs.Количество])) - SUM([Расходы])))  END ```  | дробное число / авто | нет |
| 8 | Налог  | ``` if [UnitType] = 'Общий отчет о продажах'    then if [Nalog] = 1    THEN [sdrs.Цена (со скидкой продавца, до СПП)] / 100    ELSE ([sdrs.Цена (со скидкой продавца, до СПП)] / 100) * 6 ENDELSE if [Nalog] = 1    THEN ([sdrs.Цена (со скидкой продавца, до СПП)] / [sdrs.Количество]) / 100    ELSE (([sdrs.Цена (со скидкой продавца, до СПП)] / [sdrs.Количество]) / 100) * 6 END END ```  | дробное число / авто | нет |
| 9 | Маржа | ``` if [UnitType] = 'Общий отчет о продажах'   then [Чистая прибыль] / [sdrs.Цена (со скидкой продавца, до СПП)]ELSE [Чистая прибыль] / ([sdrs.Цена (со скидкой продавца, до СПП)] / [sdrs.Количество]) END  ```  | дробное число / авто | нет |
| 10 | ROI | ``` if [UnitType] = 'Общий отчет о продажах'    then [Чистая прибыль] / SUM(IFNULL([cp.cost], 0) * [sdrs.Количество]) ELSE [Чистая прибыль] / SUM(IFNULL([cp.cost], 0)) END ```  | дробное число / авто | нет |
| 11 | Расходы| ``` SUM([Себестоимость])    + SUM([Логистика])    + SUM([Рекламные расходы])    + SUM([Комиссия ВБ])    + SUM([Платное хранение])    + SUM([Налог] ```  | дробное число / авто | нет |
| 12 | Платное хранение 1 ед. | ``` IFNULL(SUM(([pss.sum_warehousePric] / [pss.sum_barcodesCount])), 0)  ```  | дробное число / авто | нет |
| 13 | Платное хранение | ``` if [UnitType] = 'Общий отчет о продажах'    then IFNULL(SUM(([pss.sum_warehousePric] / [pss.sum_barcodesCount])), 0) * [sdrs.Количество] ELSE IFNULL(SUM(([pss.sum_warehousePric] / [pss.sum_barcodesCount])), 0) END ```  | дробное число / авто | нет |
| 14 | Рекламные расходы | ``` if [UnitType] = 'Общий отчет о продажах'    then IFNULL([ass.sum_ads], 0) ELSE IFNULL([ass.sum_ads], 0) / [sdrs.Количество] END ```  | дробное число / авто | нет |
| 15 | pss.sum_warehousePric | нет  | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 16 | sdrs.Артикул ВБ | нет  | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 17 | sdrs.Артикул продовца | нет  | строка / нет | [mp_db.unitka](#mp_db_unitka) |
| 18 | sdrs.Дата продажи | нет  | дата / нет | [mp_db.unitka](#mp_db_unitka) |
| 19 | sdrs.Цена (со скидкой продавца, до СПП) | нет  | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 20 | sdrs.Логистика | нет  | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 21 | sdrs.Комиссия ВБ | нет  | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 22 | sdrs.Штрафы | нет  | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 23 | sdrs.Платная премка | нет | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 24 | ass.date_ads | нет | дата / нет | [mp_db.unitka](#mp_db_unitka) |
| 25 | ass.nmid_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 26 | ass.views_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 27 | ass.clicks_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 28 | ass.sum_ads| нет | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 29 | ass.atbs_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 30 | ass.orders_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 31 | ass.shks_ads | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 32 | ass.sum_price_ads | нет | дробное число / нет | [mp_db.unitka](#mp_db_unitka) |
| 33 | pss.date | нет | дата / нет | [mp_db.unitka](#mp_db_unitka) |
| 34 | pss.nmId | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 35 | cp.nmID | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka) |
| 36 | cp.cost | нет | дробное число / нет | [mp_db.unitka](#mp_db_unitka) |
| 37 | sdrs.Количество | нет | дробное число / сумма | [mp_db.unitka](#mp_db_unitka) |
| 38 | pss.sum_barcodesCount | нет | дробное число / нет | [mp_db.unitka](#mp_db_unitka) |
| 39 | sdrs.Цена до скидок | нет | целое число / нет | [mp_db.unitka](#mp_db_unitka)) |

## 2. Представления
### mp_db_ads_stat_summary
**Родительская таблица** - [mp_db.advert_stats](#mp_db_advert_stats)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - date_ads, nmId

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|date_ads|[date](#mp_db_advert_stats)|Date(10,notnull)|-|
|2|nmid_ads|[nmId](#mp_db_advert_stats)|Int32(10,notnull)|-|
|3|views_ads|[views](#mp_db_advert_stats)|Int64(19,notnull)|sum|
|4|clicks_ads|[clicks](#mp_db_advert_stats)|Int64(19,notnull)|sum|
|5|sum_ads|[sum](#mp_db_advert_stats)|Float64(22,notnull)|sum|
|6|atbs_ads|[atbs](#mp_db_advert_stats)|Int64(19,notnull)|sum|
|7|orders_ads|[orders](#mp_db_advert_stats)|Int64(19,notnull)|sum|
|8|shks_ads|[shks](#mp_db_advert_stats)|Int64(19,notnull)|sum|
|9|sum_price_ads|[sum_price](#mp_db_advert_stats)|Float64(22,notnull)|sum|

### mp_db_articleadd
**Родительская таблица** - [mp_db.sales_stat](#mp_db_sales_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, supplierArticle

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmId |[nmId](#mp_db_sales_stat)|Int32(10,notnull)|-|
|2|supplierArticle|[supplierArticle](#mp_db_sales_stat)|String(notnull)|-|

### mp_db_execute_plan
**Родительская таблица** - [mp_db.plan_fact_current](#mp_db_plan_fact_current)\
**Присоединяемые таблицы** - левый джоин [mp_db.order_current](#mp_db_order_current)\
(pfc.wb_sku = oc.nmid_orders)\
**Группировка по полям** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|supplier_sku|[supplier_sku](#mp_db_plan_fact_current)|String(notnull)|-|
|2|wb_sku|[wb_sku](#mp_db_plan_fact_current)|Int32(10,notnull)|-|
|3|month|[month](#mp_db_plan_fact_current)|Date(10,notnull)|-|
|4|monthly_plan|[monthly_plan](#mp_db_plan_fact_current)|Float64(22,notnull)|-|
|5|nmid_orders|[nmid_orders](#mp_db_order_current)|Int32(10,notnull)|-|
|6|sum(total_count_orders)|[sum(total_count_orders)](#mp_db_order_current)|UInt64(20,notnull)|-|

### mp_db_kt_stat_summary
**Родительская таблица** - [mp_db.kt_stats](#mp_db_kt_stats)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmID, dt, imtName

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmID_KT|[nmID](#mp_db_kt_stats)|Int32(10,notnull)|-|
|2|date_kt|[dt](#mp_db_kt_stats)|Date(10,notnull)|-|
|3|itemname_kt|[imtName](#mp_db_kt_stats)|String(notnull)|-|
|4|sum_opencardcount_kt|[openCardCount](#mp_db_kt_stats)|Int64(19,notnull)|sum|
|5|sum_addtocartcount_kt|[addToCartCount](#mp_db_kt_stats)|Int64(19,notnull)|sum|
|6|sum_addtocartconversion_kt|[addToCartConversion](#mp_db_kt_stats)|Float64(22,notnull)|sum|
|7|sum_orderscount_kt|[ordersCount](#mp_db_kt_stats)|Int64(19,notnull)|sum|
|8|sum_orderssumrub_kt|[ordersSumRub](#mp_db_kt_stats)|Float64(22,notnull)|sum|
|9|sum_carttoorderconversion_kt|[cartToOrderConversion](#mp_db_kt_stats)|Float64(22,notnull)|sum|
|10|sum_buyoutscount_kt|[buyoutsCount](#mp_db_kt_stats)|Int64(19,notnull)|sum|
|11|sum_buyoutssumrub_kt|[buyoutsSumRub](#mp_db_kt_stats)|Float64(22,notnull)|sum|
|12|sum_buyoutpercent_kt|[buyoutPercent](#mp_db_kt_stats)|Float64(22,notnull)|sum|

### mp_db_nmid_fullstat_renamed
**Родительская таблица** - [mp_db.kt_stat_summary](#mp_db_kt_stat_summary)\
**Присоединяемые таблицы** - левый джоин [mp_db.orders_stat_summary](#mp_db_orders_stat_summary)\
(k.nmID_KT = o.nmid_orders) AND (k.date_kt = o.date_orders),\
левый джоин [mp_db.sales_stat_summary](#mp_db_sales_stat_summary)\
(k.nmID_KT = s.nmid_sales) AND (k.date_kt = s.date_sales),\
левый джоин [mp_db.ads_stat_summary](#mp_db_ads_stat_summary)\
(k.nmID_KT = a.nmid_ads) AND (k.date_kt = a.date_ads)\
левый джоин [mp_db.articleadd](#mp_db_articleadd)\
(k.nmID_KT = art.nmId)\
**Группировка по полям** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|art.supplierArticle|[art.supplierArticle](#mp_db_articleadd)|String(null)|-|
|2|ID карточки|[nmID_KT](#mp_db_kt_stat_summary)|Int32(10,notnull)|-|
|3|Дата|[date_kt](#mp_db_kt_stat_summary)|Date(10,notnull)|-|
|4|Название товара|[itemname_kt](#mp_db_kt_stat_summary)|String(notnull)|-|
|5|Переходы в карточку (КТ)|[sum_opencardcount_kt](#mp_db_kt_stat_summary)|Int64(19,notnull)|-|
|6|Положили в корзину (КТ)|[sum_addtocartcount_kt](#mp_db_kt_stat_summary)|Int64(19,notnull)|-|
|7|Заказали товаров шт. (КТ)|[sum_orderscount_kt](#mp_db_kt_stat_summary)|Int64(19,notnull)|-|
|8|Заказали на сумму  руб. (КТ)|[sum_orderssumrub_kt](#mp_db_kt_stat_summary)|Float64(22,notnull)|-|
|9|Выкупили товаров шт. (КТ)|[sum_buyoutscount_kt](#mp_db_kt_stat_summary)|Int64(19,notnull)|-|
|10|Выкупили на сумму руб. (КТ)|[sum_buyoutssumrub_kt](#mp_db_kt_stat_summary)|Float64(22,notnull)|-|
|11|Количество заказов шт. (З)|[total_count_orders](#mp_db_orders_stat_summary)|UInt64(20,null)|-|
|12|Отмененный закаказов шт. (З)|[cancelled_count_orders](#mp_db_orders_stat_summary)|UInt64(20,null)|-|
|13|Выкупленных заказов шт. (З)|[not_cancelled_count_orders](#Вmp_db_orders_stat_summary)|UInt64(20,null)|-|
|14|Сумма заказов руб. (З)|[sum_totalprice_orders](#mp_db_orders_stat_summary)|Float64(22,null)|-|
|15|Фактическая цена руб. (З)|[sum_finishedprice_orders](#mp_db_orders_stat_summary)|Float64(22,null)|-|
|16|Цена со скидкой продавца руб. (З)|[sum_pricewithdisc_orders](#mp_db_orders_stat_summary)|Float64(22,null)|-|
|17|Количество продаж шт. (П)|[total_count_sales](#mp_db_sales_stat_summary)|UInt64(20,null)|-|
|18|Сумма продаж руб. (П)|[sum_totalprice_sales](#mp_db_sales_stat_summary)|Float64(22,null)|-|
|19|К перечислению руб. (П)|[sum_forpay_sales](#mp_db_sales_stat_summary)|Float64(22,null)|-|
|20|Фактическая цена руб. (П)|[sum_finishedprice_sales](#mp_db_sales_stat_summary)|Float64(22,null)|-|
|21|Цена со скидкой продавца руб. (П)|[sum_pricewithdisc_sales](#mp_db_sales_stat_summary)|Float64(22,null)|-|
|22|Показы (Р)|[views_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|23|Клики (Р)|[clicks_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|24|Расход руб. (Р)|[sum_ads](#mp_db_ads_stat_summary)|Float64(22,null)|-|
|25|Положили в корзину шт. (Р)|[atbs_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|26|Количество заказов шт. (Р)|[orders_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|27|Кол-во заказанных товаров шт. (Р)|[shks_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|28|Сумма заказов руб. (Р)|[sum_price_ads](#mp_db_ads_stat_summary)|Float64(22,null)|-|

### mp_db_order_current
**Родительская таблица** - [mp_db.orders_stat_summary](#mp_db_orders_stat_summary)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmid_orders

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_orders|[nmid_orders](#mp_db_orders_stat_summary)|Int32(10,notnull)|-|
|2|sum(total_count_orders)|[sum(total_count_orders)](#mp_db_orders_stat_summary)|UInt64(20,notnull)|sum|

### mp_db_orders_stat_summary
**Родительская таблица** - [mp_db.orders_stat](#mp_db_orders_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, date

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_orders|[nmId](#mp_db_orders_stat)|Int32(10,notnull)|-|
|2|date_orders|[date](#mp_db_orders_stat)|Date(10,notnull)|-|
|3|total_count_orders|[count](#mp_db_orders_stat)|UInt64(20,notnull)|count|
|4|cancelled_count_orders|[isCancel = 1](#mp_db_orders_stat)|UInt64(20,notnull)|countIf(orders_stat.isCancel = 1)|
|5|not_cancelled_count_orders|[isCancel = 0](#mp_db_orders_stat)|UInt64(20,notnull)|countIf(orders_stat.isCancel = 0)|
|6|sum_totalprice_orders|[totalPrice](#mp_db_orders_stat)|Float64(22,notnull)|sum|
|7|sum_spp_orders|[spp](#mp_db_orders_stat)|Float64(22,notnull)|sum|
|8|sum_finishedprice_orders |[finishedPrice](#mp_db_orders_stat)|Float64(22,notnull)|sum|
|9|sum_pricewithdisc_orders|[priceWithDisc](#mp_db_orders_stat)|Float64(22,notnull)|sum|

### mp_db_paid_storage_summary
**Родительская таблица** - [mp_db.paid_storage](#mp_db_paid_storage)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, date

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|date|[date](#mp_db_paid_storage)|Date(10,notnull)|-|
|2|nmId|[nmId](#mp_db_paid_storage)|Int32(10,notnull)|-|
|3|sum_warehousePric|[warehousePrice](#mp_db_paid_storage)|Float64(22,notnull)|sum|
|4|sum_barcodesCount|[barcodesCount](#mp_db_paid_storaget)|Float64(22,notnull)|sum|

### mp_db_plan_fact_current
**Родительская таблица** - [mp_db.product_plan](#mp_db_product_plan)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - нет\
**Дополнительные условия** - В таблице содержатся данные у которых месяц и год совпадает с текущим

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|supplier_sku|[supplier_sku](#mp_db_product_plan)|String(notnull)|-|
|2|wb_sku|[wb_sku](#mp_db_product_plan)|Int32(10,notnull)|-|
|3|month|[month](#mp_db_product_plan)|Date(10,notnull)|-|
|4|monthly_plan|[monthly_plan](#mp_db_product_plan)|Float64(22,notnull)|-|

### mp_db_sales_detail_report_summary
**Родительская таблица** - [mp_db.sales_detail_report_stat](#mp_db_sales_detail_report_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - Дата продажи, nm_id, sa_name\
**Дополнительные условия** - В таблице содержатся данные у которых поле supplier_oper_name = Продажа

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|Артикул ВБ|[nm_id ](#mp_db_sales_detail_report_stat)|Int32(10,notnull)|-|
|2|Артикул продовца|[sa_name](#mp_db_sales_detail_report_stat)|String(notnull)|-|
|3|Дата продажи|[sale_dt](#mp_db_sales_detail_report_stat)|Date(10,notnull)|-|
|4|Количество|[quantity - return_amount](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|5|Цена до скидок|[retail_price](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|6|Цена (со скидкой продавцадо СПП)|[(retail_price_withdisc_rub * quantity) - (retail_price_withdisc_rub * return_amount)](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|7|Логистика|[delivery_rub](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|8|Комиссия ВБ|[retail_price_withdisc_rub * (commission_percent / 100)](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|9|Штрафы|[penalty](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|
|10|Платная премка|[acceptance](#mp_db_sales_detail_report_stat)|Float64(22,notnull)|sum|

### mp_db_sales_stat_summary
**Родительская таблица** - [mp_db.sales_stat](#mp_db_sales_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmid_sales, date_sales\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_sales|[nmId](#mp_db_sales_stat)|Int32(10,notnull)|-|
|2|date_sales|[date](#mp_db_sales_stat)|Date(10,notnull)|-|
|3|total_count_sales|[count](#mp_db_sales_stat)|UInt64(20,notnull)|count|
|4|sum_totalprice_sales|[totalPrice](#mp_db_sales_stat)|Float64(22,notnull)|sum|
|5|sum_discountpercent_sales|[discountPercent](#mp_db_sales_stat)|Int64(19,notnull)|sum|
|6|sum_spp_sales|[spp](#mp_db_sales_stat)|Float64(22,notnull)|sum|
|7|sum_forpay_sales|[forPay](#mp_db_sales_stat)|Float64(22,notnull)|sum|
|8|sum_finishedprice_sales|[finishedPrice](#mp_db_sales_stat)|Float64(22,notnull)|sum|
|9|sum_pricewithdisc_sales|[priceWithDisc](#mp_db_sales_stat)|Float64(22,notnull)|sum|

### mp_db_stock_size
**Родительская таблица** - [mp_db.stocks_stat](#mp_db_stocks_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - нет\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|warehouseName|[warehouseName](#mp_db_stocks_stat)|Int32(10,notnull)|-|
|2|nmId|[nmId](#mp_db_stocks_stat)|String(notnull)|-|
|3|techSize|[techSize](#mp_db_stocks_stat)|Int32(10,notnull)|-|
|4|quantity|[quantity](#qmp_db_stocks_stat)|String(notnull)|-|

### mp_db_stocks_stat_new
**Родительская таблица** - [mp_db.sales_sta](#mp_db_sales_stat)t\
**Присоединяемые таблицы** - инер джоин [mp_db.stocks_stat](#mp_db_stocks_stat) \
(s.nmId = st.nmId) AND (s.warehouseName = st.warehouseName)\
левый джоин cr - ([mp_db.orders_stat](#mp_db_orders_stat) + [mp_db.sales_stat](#mp_db_sales_stat))\
(cr.nmId = s.nmId) AND (cr.warehouseName = s.warehouseName) AND (cr.date = toDate(s.date)) AND (cr.supplierArticle = s.supplierArticle)\
**Группировка по полям** - s.date, s.warehouseName, s.nmId, s.supplierArticle, cr.totalOrders, cr.totalSales\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|Дата|[date](#mp_db_sales_stat)|Date(10,null)|-|
|2|Склад|[warehouseName](#mp_db_sales_stat)|String(null)|-|
|3|s.nmId|[nmId](#mp_db_sales_stat)|Int32(10,null)|-|
|4|Количество Продаж Всего|[nmId](#mp_db_sales_stat)|UInt64(20,null)|count|
|5|Сумма Продаж По PriceWithDisc|[priceWithDisc](#mp_db_sales_stat)|Float64(22,null)|sum|
|6|Количество Остатков|[quantity](#mp_db_stocks_stat)|Int32(10,null)|max|
|7|Количество Товаров В Пути К Клиент|[inWayToClient](#mp_db_stocks_stat)|Int32(10,null)|max|
|8|s.supplierArticle|[supplierArticle](#mp_db_sales_stat)|String(null)|-|
|9|Общее Количество Заказов|[totalOrders](#cr)|UInt64(20,null)|-|
|10|Общее Количество Продаж|[totalSales](#cr)|UInt64(20,null)|-|

### mp_db_unitka
**Родительская таблица** - [mp_db.sales_detail_report_summary](#mp_db_sales_detail_report_summary)\
**Присоединяемые таблицы** - полный джоин [mp_db.ads_stat_summary](#mp_db_ads_stat_summary)\
(sdrs.Дата продажи = ass.date_ads) AND (sdrs.Артикул ВБ = ass.nmid_ads)\
 полный джоин [mp_db.paid_storage_summary](#mp_db_paid_storage_summary)\
(sdrs.Дата продажи = pss.date) AND (sdrs.Артикул ВБ = pss.nmId)\
 полный джоин [mp_db.cost_price](#mp_db_cost_price)\
(cp.nmID = sdrs.Артикул ВБ)\
 полный джоин [mp_db.sales_stat_summary](#mp_db_sales_stat_summary)\
(sss.nmid_sales = sdrs.Артикул ВБ) AND (sdrs.Дата продажи = sss.date_sales)\
**Группировка по полям** - нет\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|sdrs.Артикул ВБ|[Артикул ВБ](#mp_db_sales_detail_report_summary)|Int32(10,null)|-|
|2|sdrs.Артикул продовца|[Артикул продовца](#mp_db_sales_detail_report_summary)|String(null)|-|
|3|sdrs.Дата продажи|[Дата продажи](#mp_db_sales_detail_report_summary)|Date(10,null)|-|
|4|sdrs.Количество|[Количество](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|5|sdrs.Цена до скидок|[Цена до скидок](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|6|sdrs.Цена (со скидкой продавцадо СПП)|[Цена (со скидкой продавцадо СПП)](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|7|sdrs.Логистика|[Логистика](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|8|sdrs.Комиссия ВБ|[Комиссия ВБ](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|9|sdrs.Штрафы|[Штрафы](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|10|sdrs.Платная премка|[Платная премка](#mp_db_sales_detail_report_summary)|Float64(22,null)|-|
|11|ass.date_ads|[date_ads](#mp_db_ads_stat_summary)|Date(10,null)|-|
|12|ass.nmid_ads|[nmid_ads](#mp_db_ads_stat_summary)|Int32(10,null)|-|
|13|ass.views_ads|[views_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|14|ass.clicks_ads|[clicks_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|15|ass.sum_ads|[sum_ads](#mp_db_ads_stat_summary)|Float64(22,null)|-|
|16|ass.atbs_ads|[atbs_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|17|ass.orders_ads|[orders_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|18|ass.shks_ads|[shks_ads](#mp_db_ads_stat_summary)|Int64(19,null)|-|
|19|ass.sum_price_ads|[sum_price_ads](#mp_db_ads_stat_summary)|Float64(22,null)|-|
|20|pss.date|[date](#mp_db_paid_storage_summary)|Date(10,null)|-|
|21|pss.nmId|[nmId](#mp_db_paid_storage_summary)|Int32(10,null)|-|
|22|pss.sum_warehousePric|[sum_warehousePric](#mp_db_paid_storage_summary)|Float64(22,null)|-|
|23|pss.sum_barcodesCount|[sum_barcodesCount](#mp_db_paid_storage_summary)|Float64(22,null)|-|
|24|cp.nmID|[nmID](#mp_db_cost_price)|Int32(10,null)|-|
|25|cp.cost|[cost](#mp_db_cost_price)|Float64(22,null)|-|   

## 3. Таблицы
### mp_db_ads_cost_history 

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|updNum|Int32(10,notnull)|Номер выставленного документа (при наличии)|
|3|updTime|DateTime(29,notnull)|Время списания|
|4|updSum|Int32(10,notnull)|Выставленная сумма в руб.|
|5|advertId|Int32(10,notnull)|Идентификатор кампании|
|6|campName|String(notnull)|Название кампании|
|7|advertType|Int32(10,notnull)|Тип кампании|
|8|paymentType|String(notnull)|Источник списания: Баланс Бонусы Счет |
|9|advertStatus|Int32(10,notnull)|Статус кампании: 4 - готова к запуску 7 - завершена 8 - отказался 9 - активна 11 - приостановлена |

### mp_db_advert_stats

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|date|DateTime(29,notnull)|Даты, за которые необходимо выдать информацию.|
|3|advertId|Int32(10,notnull)|ID кампании|
|4|appType|Int32(10,notnull)|не нашел|
|5|nmId|Int32(10,notnull)|Артикул Wildberries|
|6|views|Int32(10,notnull)|Количество просмотров. За все дни, по всем артикулам WB и платформам.|
|7|clicks|Int32(10,notnull)|Количество кликов. За все дни, по всем артикулам WB и платформам.|
|8|sum|Float32(12,notnull)|Затраты, ₽. За все дни, по всем артикулам WB и платформам.|
|9|atbs|Int32(10,notnull)|Количество добавлений товаров в корзину. За все дни, по всем артикулам WB и платформам.|
|10|orders|Int32(10,notnull)|Количество заказов. За все дни, по всем артикулам WB и платформам.|
|11|shks|Int32(10,notnull)|Количество заказанных товаров, шт. За все дни, по всем артикулам WB и платформам.|
|12|sum_price|Float32(12,notnull)|Заказов на сумму, ₽ За все дни, по всем артикулам WB и платформам.|
|13|ctr|Float32(12,notnull)|Показатель кликабельности. Отношение числа кликов к количеству показов. Выражается в процентах. За все дни, по всем артикулам WB и платформам.|
|14|cpc|Float32(12,notnull)|Средняя стоимость клика, ₽. За все дни, по всем артикулам WB и платформам.|
|15|cr|Float32(12,notnull)|CR(conversion rate) — это отношение количества заказов к общему количеству посещений кампании. За все дни, по всем артикулам WB и платформам.|
|16|name|String(notnull)|Предмет|

### mp_db_cards_content

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|vendorCode|String(notnull)|Артикул продавца|
|3|nmID|Int32(10,notnull)|Артикул Wildberries|
|4|subjectName|String(notnull)|Название объекта|
|5|brand|String(notnull)|Бренд|
|6|title|String(notnull)|Заголовок|
|7|sizes|String(notnull)|Размер|
|8|volume|Float32(12,notnull)|Количество|
|9|big_photo|String(notnull)|Фото|
|10|color|String(notnull)|Цвет|
|11|gender|String(notnull)|Пол|
|12|tags|String(notnull)|Тэги|

### mp_db_commissions

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|kgvpMarketplace|Float32(12,notnull)| |
|3|kgvpSupplier|Float32(12,notnull)| |
|4|kgvpSupplierExpress|Float32(12,notnull)| |
|5|paidStorageKgvp|Float32(12,notnull)| |
|6|parentID|Int32(10,notnull)| |
|7|parentName|String(notnull)| |
|8|subjectID|Int32(10,notnull)| |
|9|subjectName|String(notnull)| |
|10|date|DateTime(29,notnull)| |

### mp_db_cost_price

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|nmID|Int32(10,notnull)|Артикул Wildberries|
|2|cost|Float32(12,notnull)|Стоимость|

### mp_db_kt_stats

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|nmID|Int32(10,notnull)|Артикул Wildberries|
|3|imtName|String(notnull)| |
|4|vendorCode|String(notnull)|Артикул продавца|
|5|dt|DateTime(29,notnull)|Дата|
|6|openCardCount|Int32(10,notnull)|Переходы в карточку товара|
|7|addToCartCount|Int32(10,notnull)|Положили в корзину, шт|
|8|ordersCount|Int32(10,notnull)|Заказали товаров, шт.|
|9|ordersSumRub|Float32(12,notnull)|Заказали на сумму, ₽|
|10|buyoutsCount|Int32(10,notnull)|Выкупили товаров, шт|
|11|buyoutsSumRub|Float32(12,notnull)|Выкупили на сумму, ₽|
|12|buyoutPercent|Float32(12,notnull)|Процент выкупа, % (Какой процент посетителей, заказавших товар, его выкупили. Без учёта товаров, которые еще доставляются покупателю)|
|13|addToCartConversion|Float32(12,notnull)|Конверсия в корзину, % (Какой процент посетителей, открывших карточку товара, добавили товар в корзину)|
|14|cartToOrderConversion|Float32(12,notnull)|Конверсия в заказ, % (Какой процент посетителей, добавивших товар в корзину, сделали заказ)|

### mp_db_orders_stat

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|date|DateTime(29,notnull)| |
|3|lastChangeDate|DateTime(29,notnull)|Дата и время обновления информации в сервисе. |
|4|warehouseName|String(notnull)|Склад отгрузки|
|5|countryName|String(notnull)|Страна|
|6|oblastOkrugName|String(notnull)|Округ|
|7|regionName|String(notnull)|Регион|
|8|supplierArticle|String(notnull)|Артикул продавца|
|9|nmId|Int32(10,notnull)|Артикул WB|
|10|barcode|String(notnull)|Баркод|
|11|category|String(notnull)|Категория|
|12|subject|String(notnull)|Предмет|
|13|brand|String(notnull)|Бренд|
|14|techSize|String(notnull)|Размер товара|
|15|incomeID|Int32(10,notnull)|Номер поставки|
|16|isSupply|Bool(notnull)|Договор поставки|
|17|isRealization|Bool(notnull)|Договор реализации|
|18|totalPrice|Float32(12,notnull)|Цена без скидок|
|19|discountPercent|Float32(12,notnull)|Скидка продавца|
|20|spp|Float32(12,notnull)|Скидка WB|
|21|finishedPrice|Float32(12,notnull)|Цена с учетом всех скидок, кроме суммы по WB Кошельку|
|22|priceWithDisc|Float32(12,notnull)|Цена со скидкой продавца (= totalPrice * (1 - discountPercent/100))|
|23|isCancel|Bool(notnull)|Отмена заказа. true - заказ отменен|
|24|cancelDate|DateTime(29,notnull)|Дата и время отмены заказа|
|25|orderType|String(notnull)|Тип заказа|
|26|sticker|String(notnull)|Идентификатор стикера|
|27|gNumber|String(notnull)|Номер заказа|
|28|srid|String(notnull)|Уникальный идентификатор заказа.|

### mp_db_paid_storage

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|date|String(notnull)|Дата, за которую был расчёт или перерасчёт|
|3|logWarehouseCoef|Float32(12,notnull)|Коэффициент логистики и хранения|
|4|officeId|Int32(10,notnull)|ID склада|
|5|warehouse|String(notnull)|Название склада|
|6|warehouseCoef|Float32(12,notnull)|Коэффициент склада|
|7|giId|Int32(10,notnull)|ID поставки|
|8|chrtId|Int32(10,notnull)|Идентификатор размера для этого артикула Wildberries|
|9|size|String(notnull)|Размер (techSize в карточке товара)|
|10|barcode|String(notnull)|Баркод|
|11|subject|String(notnull)|Предмет|
|12|brand|String(notnull)|Бренд|
|13|vendorCode|String(notnull)|Артикул продавца|
|14|nmId|Int32(10,notnull)|Артикул Wildberries|
|15|volume|Float32(12,notnull)|Объём товара|
|16|calcType|String(notnull)|Способ расчёта|
|17|warehousePrice|Float32(12,notnull)|Сумма хранения|
|18|barcodesCount|Int32(10,notnull)|Количество единиц товара (штук), подлежащих тарифицированию за расчётные сутки|
|19|palletPlaceCode|Int32(10,notnull)|Код паллетоместа|
|20|palletCount|Float32(12,notnull)|Количество паллет|
|21|originalDate|String(notnull)|Если был перерасчёт, это дата первоначального расчёта. Если перерасчёта не было, совпадает с date|
|22|loyaltyDiscount|Float32(12,notnull)|Скидка программы лояльности, ₽|
|23|tariffFixDate|String(notnull)|Дата фиксации тарифа|
|24|tariffLowerDate|String(notnull)|Дата понижения тарифа|

### mp_db_product_plan

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|supplier_sku|String(notnull)| |
|2|wb_sku|String(notnull)| |
|3|monthly_plan|UInt32(10,notnull)| |
|4|month|Date(0,notnull)| |

### mp_db_sales_detail_report_stat

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|realizationreport_id|Int32(10,notnull)|Номер отчёта|
|3|date_from|DateTime(29,notnull)|Дата начала отчётного периода|
|4|date_to|DateTime(29,notnull)|Дата конца отчётного периода|
|5|create_dt|DateTime(29,notnull)|Дата формирования отчёта|
|6|currency_name|String(notnull)|Валюта отчёта|
|7|suppliercontract_code|String(notnull)|Договор|
|8|rrd_id|Int32(10,notnull)|Номер строки|
|9|gi_id|Int32(10,notnull)|Номер поставки|
|10|subject_name|String(notnull)|Предмет|
|11|nm_id|Int32(10,notnull)|Артикул WB|
|12|brand_name|String(notnull)|Бренд|
|13|sa_name|String(notnull)|Артикул продавца|
|14|ts_name|String(notnull)|Размер|
|15|barcode|String(notnull)|Баркод|
|16|doc_type_name|String(notnull)|Тип документа|
|17|quantity|Int32(10,notnull)|Количество|
|18|retail_price|Float32(12,notnull)|Цена розничная|
|19|retail_amount|Float32(12,notnull)|Сумма продаж (возвратов)|
|20|sale_percent|Float32(12,notnull)|Согласованная скидка|
|21|commission_percent|Float32(12,notnull)|Процент комиссии|
|22|office_name|String(notnull)|Склад|
|23|supplier_oper_name|String(notnull)|Обоснование для оплаты|
|24|order_dt|DateTime(29,notnull)|Дата заказа. Присылается с явным указанием часового пояса|
|25|sale_dt|DateTime(29,notnull)|Дата продажи. Присылается с явным указанием часового пояса|
|26|rr_dt|DateTime(29,notnull)|Дата операции. Присылается с явным указанием часового пояса|
|27|shk_id|Int32(10,notnull)|Штрих-код|
|28|retail_price_withdisc_rub|Float32(12,notnull)|Цена розничная с учетом согласованной скидки|
|29|delivery_amount|Float32(12,notnull)|Количество доставок|
|30|return_amount|Float32(12,notnull)|Количество возвратов|
|31|delivery_rub|Float32(12,notnull)|Стоимость логистики|
|32|gi_box_type_name|String(notnull)|Тип коробов|
|33|product_discount_for_report|Float32(12,notnull)|Согласованный продуктовый дисконт|
|34|supplier_promo|Float32(12,notnull)|Промокод|
|35|rid|Int32(10,notnull)|Уникальный идентификатор заказа|
|36|ppvz_spp_prc|Float32(12,notnull)|Скидка постоянного покупателя|
|37|ppvz_kvw_prc_base|Float32(12,notnull)|Размер кВВ без НДС, % базовый|
|38|ppvz_kvw_prc|Float32(12,notnull)|Итоговый кВВ без НДС, %|
|39|sup_rating_prc_up|Float32(12,notnull)|Размер снижения кВВ из-за рейтинга|
|40|is_kgvp_v2|Int32(10,notnull)|Размер снижения кВВ из-за акции|
|41|ppvz_sales_commission|Float32(12,notnull)|Вознаграждение с продаж до вычета услуг поверенного, без НДС|
|42|ppvz_for_pay|Float32(12,notnull)|К перечислению продавцу за реализованный товар|
|43|ppvz_reward|Float32(12,notnull)|Возмещение за выдачу и возврат товаров на ПВЗ|
|44|acquiring_fee|Float32(12,notnull)|Возмещение издержек по эквайрингу.|
|45|acquiring_bank|String(notnull)|Наименование банка-эквайера|
|46|ppvz_vw|Float32(12,notnull)|Вознаграждение WB без НДС|
|47|ppvz_vw_nds|Float32(12,notnull)|НДС с вознаграждения WB|
|48|ppvz_office_id|Int32(10,notnull)|Номер офиса|
|49|ppvz_office_name|String(notnull)|Наименование офиса доставки|
|50|ppvz_supplier_id|Int32(10,notnull)|Номер партнера|
|51|ppvz_supplier_name|String(notnull)|Партнер|
|52|ppvz_inn|String(notnull)|ИНН партнера|
|53|declaration_number|String(notnull)|Номер таможенной декларации|
|54|bonus_type_name|String(notnull)|Обоснование штрафов и доплат.Поле будет в ответе при наличии значения|
|55|sticker_id|String(notnull)|Цифровое значение стикера, который клеится на товар в процессе сборки заказа по схеме "Маркетплейс"|
|56|site_country|String(notnull)|Страна продажи|
|57|penalty|Float32(12,notnull)|Штрафы|
|58|additional_payment|Float32(12,notnull)|Доплаты|
|59|rebill_logistic_cost|Float32(12,notnull)|Возмещение издержек по перевозке. Поле будет в ответе при наличии значения|
|60|rebill_logistic_org|String(notnull)|Организатор перевозки. Поле будет в ответе при наличии значения|
|61|kiz|String(notnull)|Код маркировки.Поле будет в ответе при наличии значения|
|62|storage_fee|Float32(12,notnull)|Стоимость хранения|
|63|deduction|Float32(12,notnull)|Прочие удержания/выплаты|
|64|acceptance|Float32(12,notnull)|Стоимость платной приёмки|
|65|srid|String(notnull)|Уникальный идентификатор заказа.Srid равен rid в ответах методов сборочных заданий.|
|66|report_type|Int32(10,notnull)|Тип отчёта: 1 — стандартный 2 — для уведомления о выкупе|

### mp_db_sales_stat

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|date|DateTime(29,notnull)|Дата и время продажи. Это поле соответствует параметру dateFrom в запросе, если параметр flag=1. Если часовой пояс не указан, то берется Московское время (UTC+3)|
|3|lastChangeDate|DateTime(29,notnull)|Дата и время обновления информации в сервисе. Это поле соответствует параметру dateFrom в запросе, если параметр flag=0 или не указан. Если часовой пояс не указан, то берется Московское время (UTC+3)|
|4|warehouseName|String(notnull)|Склад отгрузки|
|5|countryName|String(notnull)|Страна|
|6|oblastOkrugName|String(notnull)|Округ|
|7|regionName|String(notnull)|Регион|
|8|supplierArticle|String(notnull)|Артикул продавца|
|9|nmId|Int32(10,notnull)|Артикул WB|
|10|barcode|String(notnull)|Баркод|
|11|category|String(notnull)|Категория|
|12|subject|String(notnull)|Предмет|
|13|brand|String(notnull)|Бренд|
|14|techSize|String(notnull)|Размер товара|
|15|incomeID|Int32(10,notnull)|Номер поставки|
|16|isSupply|Bool(notnull)|Договор поставки|
|17|isRealization|Bool(notnull)|Договор реализации|
|18|totalPrice|Float32(12,notnull)|Цена без скидок|
|19|discountPercent|Int32(10,notnull)|Скидка продавца|
|20|spp|Float32(12,notnull)|Скидка WB|
|21|paymentSaleAmount|Float32(12,notnull)|Оплачено с WB Кошелька|
|22|forPay|Float32(12,notnull)|К перечислению продавцу|
|23|finishedPrice|Float32(12,notnull)|Фактическая цена с учетом всех скидок (к взиманию с покупателя)|
|24|priceWithDisc|Float32(12,notnull)|Цена со скидкой продавца, от которой считается сумма к перечислению продавцу forPay (= totalPrice * (1 - discountPercent/100))|
|25|saleID|String(notnull)|Уникальный идентификатор продажи/возврата S********** — продажа R********** — возврат (на склад WB)|
|26|orderType|String(notnull)|Тип заказа|
|27|sticker|String(notnull)|Идентификатор стикера|
|28|gNumber|String(notnull)|Номер заказа|
|29|srid|String(notnull)|Уникальный идентификатор заказа|

### mp_db_stocks_stat

|Номер столбца|Название столбца|Тип столбца|Описание|
|:---:|:---:|:---:|:---:|
|1|id|Int32(10,notnull)|Идентификатор записи|
|2|lastChangeDate|DateTime(29,notnull)| |
|3|warehouseName|String(notnull)| |
|4|supplierArticle|String(notnull)| |
|5|nmId|Int32(10,notnull)| |
|6|barcode| | |
|7|quantity|Int32(10,notnull)| |
|8|inWayToClient|Int32(10,notnull)| |
|9|inWayFromClient|Int32(10,notnull)| |
|10|quantityFull|Int32(10,notnull)| |
|11|category|String(notnull)| |
|12|subject|String(notnull)| |
|13|brand|String(notnull)| |
|14|techSize|String(notnull)| |
|15|Price|Float32(12,notnull)| |
|16|Discount|Float32(12,notnull)| |
|17|isSupply|Bool(notnull)| |
|18|isRealization|Bool(notnull)| |
|19|SCCode|String(notnull)| |
