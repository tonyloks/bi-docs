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
1. [mp_db.ads_stat_summary](#mp_db.ads_stat_summary);
1. [mp_db.articleadd](#mp_db.articleadd);
1. [mp_db.execute_plan](#mp_db.execute_plan);
1. [mp_db.kt_stat_summary](#mp_db.kt_stat_summary);
1. [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed);
1. [mp_db.order_current](#mp_db.order_current);
1. [mp_db.orders_stat_summary](#mp_db.orders_stat_summary);
1. [mp_db.paid_storage_summary](#mp_db.paid_storage_summary);
1. [mp_db.plan_fact_current](#mp_db.plan_fact_current);
1. [mp_db.sales_detail_report_summary](#mp_db.sales_detail_report_summary);
1. [mp_db.sales_stat_summary](#mp_db.sales_stat_summary);
1. [mp_db.stock_size](#mp_db.stock_size);
1. [mp_db.stocks_stat_new](#mp_db.stocks_stat_new);
1. [mp_db.unitka](#mp_db.unitka).
 # 3. Таблицы
Список таблиц:
1. [mp_db.ads_cost_history](#mp_db.ads_cost_history);
1. [mp_db.advert_stats](#mp_db.advert_stats);
1. [mp_db.cards_content](#mp_db.cards_content);
1. [mp_db.commissions](#mp_db.commissions);
1. [mp_db.cost_price](#mp_db.cost_price);
1. [mp_db.kt_stats](#mp_db.kt_stats);
1. [mp_db.orders_stat](#mp_db.orders_stat);
1. [mp_db.paid_storage](#mp_db.paid_storage);
1. [mp_db.product_plan](#mp_db.product_plan);
1. [mp_db.sales_detail_report_stat](#mp_db.sales_detail_report_stat);
1. [mp_db.sales_stat](#mp_db.sales_stat);
1. [mp_db.stocks_stat](#mp_db.stocks_stat).

    ## 1. Датасеты

### Выкупы
**Таблица / представление** - [mp_db.kt_stats](#mp_db.kt_stats)\
**Есть ли расчетные поля** - нет\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | id   | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 2 | nmID | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 3 | imtName   | нет | Строка / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 4 | vendorCode   | нет | Строка / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 5 | dt   | нет | дата и время / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 6 | openCardCount   | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 7 | addToCartCount   | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 8 | ordersCount   | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 9 | ordersSumRub   | нет | Дробное число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 10 | buyoutsCount   | нет | Целое число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 11 | buyoutsSumRub   | нет | Дробное число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 12 | buyoutPercent   | нет | Дробное число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 13 | addToCartConversion   | нет | Дробное число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |
| 14 | cartToOrderConversion   | нет | Дробное число / нет | [mp_db.kt_stats](#mp_db.kt_stats) |


### Основной_датасет
**Таблица / представление** - [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed)\
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
| 19 |  CPO, руб.  | ``` IF [Количество заказов, шт. (Р)] != 0     THEN [Сумма заказов, руб. (Р)]/[Количество заказов, шт. (Р)] ELSE NULL END  ```  | дробное число / авто | нет |
| 20 |  CTR, %  | ``` IF [Показы (Р)] != 0   THEN [Клики (Р)]/[Показы (Р)] ELSE NULL END ```  | дробное число / авто | нет |
| 21 |  Скалированная дата | ``` IF [scale_date] = 'День'     then [Дата] ELSEIF [scale_date] = 'Неделя'     then DATETRUNC([Дата],'week') ELSEIF [scale_date] = 'Месяц'     then DATETRUNC([Дата],'month') ELSEIF [scale_date] = 'Квартал'     then DATETRUNC([Дата],'quarter') ELSEIF [scale_date] = 'Год'     then DATETRUNC([Дата],'year') END  ```  | дата / нет | нет |
| 22 |   Выкуп, % | ``` if [Заказали товаров, шт. (КТ)] != 0     then sum([Выкупили товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) / sum([Заказали товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) else   NULL     end ```  | дробное число / авто | нет |
| 23 |   art.supplierArticle | нет | строка / нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 24 |  ID карточки  | нет | целое число / нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 25 |  Дата  | нет | дата / нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 26 |  Название товара  | нет | строка / нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 27 |   Переходы в карточку (КТ) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 28 |   Положили в корзину (КТ) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 29 |   Заказали товаров, шт. (КТ) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 30 |   Заказали на сумму, руб. (КТ) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 31 |   Выкупили товаров, шт. (КТ) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 32 |   Выкупили на сумму, руб. (КТ) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 33 |   Количество заказов, шт. (З) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 34 |   Отмененный закаказов, шт. (З) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 35 |   Выкупленных заказов, шт. (З) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 36 |   Сумма заказов, руб. (З) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 37 |   Фактическая цена, руб. (З) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 38 |   Цена со скидкой продавца, руб. (З) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 39 |   Количество продаж, шт. (П) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 40 |   Сумма продаж, руб. (П) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 41 |   К перечислению, руб. (П) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 42 |   Фактическая цена, руб. (П) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 43 |   Цена со скидкой продавца, руб. (П) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 44 |   Показы (Р) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 45 |   Клики (Р) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 46 |   Расход, руб. (Р) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 47 |   Положили в корзину, шт. (Р) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 48 |   Количество заказов, шт. (Р) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 49 |   Кол-во заказанных товаров, шт. (Р) | нет | целое число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 50 |   Сумма заказов, руб. (Р) | нет | дробное число / сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |

### Остатки
**Таблица / представление** - [mp_db.stocks_stat_new](#mp_db.stocks_stat_new)\
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
| 20 | Дата  | нет  | дата / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 21 | Склад | нет | строка / нет |[mp_db.stocks_stat_new](#mp_db.stocks_stat_new)|
| 22 | s.nmId | нет | целое число / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 23 |  Количество Продаж Всего | нет | целое число / сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 24 |  Сумма Продаж По PriceWithDisc  | нет | дробное число / сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 25 | Количество Остатков  | нет | целое число / среднее | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 26 | Количество Товаров В Пути К Клиент | нет | целое число / среднее | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 27 | s.supplierArticle | нет | строка / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 28 | Общее Количество Заказов | нет | целое число / сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 29 | Общее Количество Продаж | нет | целое число / сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |

### Остатки_размеры
**Таблица / представление** - [mp_db.stock_size](#mp_db.stock_size)\
**Есть ли расчетные поля** - нет\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | Карточка товара | ``` [nmId] ``` | строка / нет | нет |
| 2 | Ссылка | ``` URL('https://www.wildberries.ru/catalog/'+ str([Карточка товара]) + '/detail.aspx', str([Карточка товара])) ``` | разметка / нет | нет |
| 3 | warehouseName | нет  | строка / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 4 | nmId | нет  | целое число / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 5 | techSize | нет  | строка / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 6 | quantity | нет  | целое число / нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |

### План факт
**Таблица / представление** - левое соединение 
[mp_db.plan_fact_current](#mp_db.plan_fact_current) - [mp_db.order_current](#mp_db.plan_fact_current)\
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
| 10 | supplier_sku| нет |  строка / нет  | [mp_db.plan_fact_current](#mp_db.plan_fact_current) |
| 11 | wb_sku | нет | целое число / нет | [mp_db.plan_fact_current](#mp_db.plan_fact_current) |
| 12 | month | нет | дата / нет | [mp_db.plan_fact_current](#mp_db.plan_fact_current) |
| 13 | monthly_plan| нет | дата / авто | [mp_db.plan_fact_current](#mp_db.plan_fact_current) |
| 14 | nmid_orders| нет | целое число / нет | [mp_db.order_current](#mp_db.plan_fact_current) |
| 15 | sum(total_count_orders) | нет | целое число / нет | [mp_db.order_current](#mp_db.plan_fact_current) |

### Юнит_экономика
**Таблица / представление** - [mp_db.unitka](#mp_db.unitka)\
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
| 15 | pss.sum_warehousePric | нет  | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 16 | sdrs.Артикул ВБ | нет  | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 17 | sdrs.Артикул продовца | нет  | строка / нет | [mp_db.unitka](#mp_db.unitka) |
| 18 | sdrs.Дата продажи | нет  | дата / нет | [mp_db.unitka](#mp_db.unitka) |
| 19 | sdrs.Цена (со скидкой продавца, до СПП) | нет  | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 20 | sdrs.Логистика | нет  | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 21 | sdrs.Комиссия ВБ | нет  | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 22 | sdrs.Штрафы | нет  | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 23 | sdrs.Платная премка | нет | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 24 | ass.date_ads | нет | дата / нет | [mp_db.unitka](#mp_db.unitka) |
| 25 | ass.nmid_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 26 | ass.views_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 27 | ass.clicks_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 28 | ass.sum_ads| нет | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 29 | ass.atbs_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 30 | ass.orders_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 31 | ass.shks_ads | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 32 | ass.sum_price_ads | нет | дробное число / нет | [mp_db.unitka](#mp_db.unitka) |
| 33 | pss.date | нет | дата / нет | [mp_db.unitka](#mp_db.unitka) |
| 34 | pss.nmId | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 35 | cp.nmID | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka) |
| 36 | cp.cost | нет | дробное число / нет | [mp_db.unitka](#mp_db.unitka) |
| 37 | sdrs.Количество | нет | дробное число / сумма | [mp_db.unitka](#mp_db.unitka) |
| 38 | pss.sum_barcodesCount | нет | дробное число / нет | [mp_db.unitka](#mp_db.unitka) |
| 39 | sdrs.Цена до скидок | нет | целое число / нет | [mp_db.unitka](#mp_db.unitka)) |

## 2. Представления
### mp_db.ads_stat_summary
**Родительская таблица** - [mp_db.advert_stats](#mp_db.advert_stats)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - date_ads, nmId

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|date_ads|[date_ads](#date_ads)|Date(10,notnull)|-|
|2|nmid_ads|[nmid_ads](#nmid_ads)|Int32(10,notnull)|-|
|3|views_ads|[views_ads](#views_ads)|Int64(19,notnull)|sum|
|4|clicks_ads|[nmid_ads](#nmid_ads)|Int64(19,notnull)|sum|
|5|sum_ads|[views_ads](#views_ads)|Float64(22,notnull)|sum|
|6|atbs_ads|[nmid_ads](#nmid_ads)|Int64(19,notnull)|sum|
|7|orders_ads|[views_ads](#views_ads)|Int64(19,notnull)|sum|
|8|shks_ads|[nmid_ads](#nmid_ads)|Int64(19,notnull)|sum|
|9|sum_price_ads|[views_ads](#views_ads)|Float64(22,notnull)|sum|

### mp_db.articleadd
**Родительская таблица** - [mp_db.sales_stat](#mp_db.sales_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, supplierArticle

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_ads|[nmid_ads](#nmid_ads)|Int32(10,notnull)|-|
|2|supplierArticle|[supplierArticle](#supplierArticle)|String(notnull)|-|

### mp_db.execute_plan
**Родительская таблица** - [mp_db.plan_fact_current](#mp_db.plan_fact_current)\
**Присоединяемые таблицы** - левый джоин [mp_db.order_current](#mp_db.order_current)\
(pfc.wb_sku = oc.nmid_orders)\
**Группировка по полям** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|supplier_sku|[supplier_sku](#supplier_sku)|String(notnull)|-|
|2|wb_sku|[wb_sku](#wb_sku)|Int32(10,notnull)|-|
|3|month|[month](#month)|Date(10,notnull)|-|
|4|monthly_plan|[monthly_plan](#monthly_plan)|Float64(22,notnull)|-|
|5|nmid_orders|[nmid_orders](#nmid_orders)|Int32(10,notnull)|-|
|6|sum(total_count_orders)|[sum(total_count_orders)](#sum(total_count_orders))|UInt64(20,notnull)|-|

### mp_db.kt_stat_summary
**Родительская таблица** - [mp_db.kt_stats](#mp_db.kt_stats)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmID, dt, imtName

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmID_KT|[nmID_KT](#nmID_KT)|Int32(10,notnull)|-|
|2|date_kt|[date_kt](#date_kt)|Date(10,notnull)|-|
|3|itemname_kt|[itemname_kt](#itemname_kt)|String(notnull)|-|
|4|sum_opencardcount_kt|[itemname_kt](#itemname_kt)|Int64(19,notnull)|sum|
|5|sum_addtocartcount_kt|[sum_addtocartcount_kt](#sum_addtocartcount_kt)|Int64(19,notnull)|sum|
|6|sum_addtocartconversion_kt|[sum_addtocartconversion_kt](#sum_addtocartconversion_kt)|Float64(22,notnull)|sum|
|7|sum_orderscount_kt|[sum_orderscount_kt](#sum_orderscount_kt)|Int64(19,notnull)|sum|
|8|sum_orderssumrub_kt|[sum_orderssumrub_kt](#sum_orderssumrub_kt)|Float64(22,notnull)|sum|
|9|sum_carttoorderconversion_kt|[sum_carttoorderconversion_kt](#sum_carttoorderconversion_kt)|Float64(22,notnull)|sum|
|10|sum_buyoutscount_kt|[sum_buyoutscount_kt](#sum_buyoutscount_kt)|Int64(19,notnull)|sum|
|11|sum_buyoutssumrub_kt|[sum_buyoutssumrub_kt](#sum_buyoutssumrub_kt)|Float64(22,notnull)|sum|
|12|sum_buyoutpercent_kt|[sum_buyoutpercent_kt](#sum_buyoutpercent_kt)|Float64(22,notnull)|sum|

### mp_db.nmid_fullstat_renamed
**Родительская таблица** - [mp_db.kt_stat_summary](#mp_db.kt_stat_summary)\
**Присоединяемые таблицы** - левый джоин [mp_db.orders_stat_summary](#mp_db.orders_stat_summary)\
(k.nmID_KT = o.nmid_orders) AND (k.date_kt = o.date_orders),\
левый джоин [mp_db.sales_stat_summary](#mp_db.sales_stat_summary)\
(k.nmID_KT = s.nmid_sales) AND (k.date_kt = s.date_sales),\
левый джоин [mp_db.ads_stat_summary](#mp_db.ads_stat_summary)\
(k.nmID_KT = a.nmid_ads) AND (k.date_kt = a.date_ads)\
левый джоин [mp_db.articleadd](#mp_db.articleadd)\
(k.nmID_KT = art.nmId)\
**Группировка по полям** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|art.supplierArticle|[art.supplierArticle](#art.supplierArticle)|Nullable(null)|-|
|2|ID карточки|[ID карточки](#ID карточки)|Int32(10,notnull)|-|
|3|Дата|[Дата](#Дата)|Date(10,notnull)|-|
|4|Название товара|[Название товара](#Название товара)|String(notnull)|-|
|5|Переходы в карточку (КТ)|[Переходы в карточку (КТ)](#Переходы в карточку (КТ))|Int64(19,notnull)|-|
|6|Положили в корзину (КТ)|[Положили в корзину (КТ)](#Положили в корзину (КТ))|Int64(19,notnull)|-|
|7|Заказали товаров шт. (КТ)|[Заказали товаров шт. (КТ)](#Заказали товаров шт. (КТ))|Int64(19,notnull)|-|
|8|Заказали на сумму  руб. (КТ)|[Заказали на сумму  руб. (КТ)](#Заказали на сумму  руб. (КТ))|Float64(22,notnull)|-|
|9|Выкупили товаров шт. (КТ)|[Выкупили товаров шт. (КТ)](#Выкупили товаров шт. (КТ))|Int64(19,notnull)|-|
|10|Выкупили на сумму руб. (КТ)|[Выкупили на сумму руб. (КТ)](#Выкупили на сумму руб. (КТ))|Float64(22,notnull)|-|
|11|Количество заказов шт. (З)|[Количество заказов шт. (З)](#Количество заказов шт. (З))|Nullable(20,null)|-|
|12|Отмененный закаказов шт. (З)|[Отмененный закаказов шт. (З)](#Отмененный закаказов шт. (З))|Nullable(20,null)|-|
|13|Выкупленных заказов шт. (З)|[Выкупленных заказов шт. (З)](#Выкупленных заказов шт. (З))|Nullable(20,null)|-|
|14|Сумма заказов руб. (З)|[Сумма заказов руб. (З)](#Сумма заказов руб. (З))|Nullable(22,null)|-|
|15|Фактическая цена руб. (З)|[Фактическая цена руб. (З)](#Фактическая цена руб. (З))|Nullable(22,null)|-|
|16|Цена со скидкой продавца руб. (З)|[Цена со скидкой продавца руб. (З)](#Цена со скидкой продавца руб. (З))|Nullable(22,null)|-|
|17|Количество продаж шт. (П)|[Количество продаж шт. (П)](#Количество продаж шт. (П))|Nullable(20,null)|-|
|18|Сумма продаж руб. (П)|[Сумма продаж руб. (П)](#Сумма продаж руб. (П))|Nullable(22,null)|-|
|19|К перечислению руб. (П)|[К перечислению руб. (П)](#К перечислению руб. (П))|Nullable(22,null)|-|
|20|Фактическая цена руб. (П)|[Фактическая цена руб. (П)](#Фактическая цена руб. (П))|Nullable(22,null)|-|
|21|Цена со скидкой продавца руб. (П)|[Цена со скидкой продавца руб. (П)](#Цена со скидкой продавца руб. (П))|Nullable(22,null)|-|
|22|Показы (Р)|[Показы (Р)](#Показы (Р))|Nullable(19,null)|-|
|23|Клики (Р)|[Клики (Р)](#Клики (Р))|Nullable(19,null)|-|
|24|Расход руб. (Р)|[Расход руб. (Р)](#Расход руб. (Р))|Nullable(22,null)|-|
|25|Положили в корзину шт. (Р)|[Положили в корзину шт. (Р)](#Положили в корзину шт. (Р))|Nullable(19,null)|-|
|26|Количество заказов шт. (Р)|[Количество заказов шт. (Р)](#Количество заказов шт. (Р))|Nullable(19,null)|-|
|27|Кол-во заказанных товаров шт. (Р)|[Кол-во заказанных товаров шт. (Р)](#Кол-во заказанных товаров шт. (Р))|Nullable(19,null)|-|
|28|Сумма заказов руб. (Р)|[Сумма заказов руб. (Р)](#Сумма заказов руб. (Р))|Nullable(22,null)|-|

### mp_db.order_current
**Родительская таблица** - [mp_db.orders_stat_summary](#mp_db.orders_stat_summary)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmid_orders

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_orders|[nmid_orders](#nmid_orders)|Int32(10,notnull)|-|
|2|sum(total_count_orders)|[sum(total_count_orders)](#sum(total_count_orders))|UInt64(20,notnull)|sum|

### mp_db.orders_stat_summary
**Родительская таблица** - [mp_db.orders_stat](#mp_db.orders_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, date

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_orders|[nmid_orders](#nmid_orders)|Int32(10,notnull)|-|
|2|date_orders|[date_orders](#date_orders)|Date(10,notnull)|-|
|3|total_count_orders|[total_count_orders](#total_count_orders)|UInt64(20,notnull)|count|
|4|cancelled_count_orders|[cancelled_count_orders](#cancelled_count_orders)|UInt64(20,notnull)|countIf(orders_stat.isCancel = 1)|
|5|not_cancelled_count_orders|[not_cancelled_count_orders](#not_cancelled_count_orders)|UInt64(20,notnull)|countIf(orders_stat.isCancel = 0)|
|6|sum_totalprice_orders|[sum_totalprice_orders](#sum_totalprice_orders)|Float64(22,notnull)|sum|
|7|sum_spp_orders|[sum_spp_orders](#sum_spp_orders)|Float64(22,notnull)|sum|
|8|sum_finishedprice_orders|[sum_finishedprice_orders](#sum_finishedprice_orders)|Float64(22,notnull)|sum|
|9|sum_pricewithdisc_orders|[sum_pricewithdisc_orders](#sum_pricewithdisc_orders)|Float64(22,notnull)|sum|

### mp_db.paid_storage_summary
**Родительская таблица** - [mp_db.paid_storage](#mp_db.paid_storage)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmId, date

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|date|[date](#date)|Date(10,notnull)|-|
|2|nmId|[nmId](#nmId)|Int32(10,notnull)|-|
|3|sum_warehousePric|[sum_warehousePric](#sum_warehousePric)|Float64(22,notnull)|sum|
|4|sum_barcodesCount|[sum_barcodesCount](#sum_barcodesCount)|Float64(22,notnull)|sum|

### mp_db.plan_fact_current
**Родительская таблица** - [mp_db.product_plan](#mp_db.product_plan)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - нет\
**Дополнительные условия** - В таблице содержатся данные у которых месяц и год совпадает с текущим

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|supplier_sku|[supplier_sku](#supplier_sku)|String(notnull)|-|
|2|wb_sku|[wb_sku](#wb_sku)|Int32(10,notnull)|-|
|3|month|[month](#month)|Date(10,notnull)|-|
|4|monthly_plan|[monthly_plan](#monthly_plan)|Float64(22,notnull)|-|

### mp_db.sales_detail_report_summary
**Родительская таблица** - [mp_db.sales_detail_report_stat](#mp_db.sales_detail_report_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - Дата продажи, nm_id, sa_name\
**Дополнительные условия** - В таблице содержатся данные у которых поле supplier_oper_name = Продажа

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|Артикул ВБ|[Артикул ВБ](#Артикул ВБ)|Int32(10,notnull)|-|
|2|Артикул продовца|[Артикул продовца](#Артикул продовца)|String(notnull)|-|
|3|Дата продажи|[Дата продажи](#Дата продажи)|Date(10,notnull)|-|
|4|Количество|[Количество](#Количество)|Float64(22,notnull)|sum|
|5|Цена до скидок|[Цена до скидок](#Цена до скидок)|Float64(22,notnull)|sum|
|6|Цена (со скидкой продавцадо СПП)|[Цена (со скидкой продавцадо СПП)](#Цена (со скидкой продавцадо СПП))|Float64(22,notnull)|sum|
|7|Логистика|[Логистика](#Логистика)|Float64(22,notnull)|sum|
|8|Комиссия ВБ|[Комиссия ВБ](#Комиссия ВБ)|Float64(22,notnull)|sum|
|9|Штрафы|[Штрафы](#Штрафы)|Float64(22,notnull)|sum|
|10|Платная премка|[Платная премка](#Платная премка)|Float64(22,notnull)|sum|

### mp_db.sales_stat_summary
**Родительская таблица** - [mp_db.sales_stat](#mp_db.sales_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - nmid_sales, date_sales\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|nmid_sales|[nmid_sales](#nmid_sales)|Int32(10,notnull)|-|
|2|date_sales|[date_sales](#date_sales)|Date(10,notnull)|-|
|3|total_count_sales|[total_count_sales](#total_count_sales)|UInt64(20,notnull)|count|
|4|sum_totalprice_sales|[sum_totalprice_sales](#sum_totalprice_sales)|Float64(22,notnull)|sum|
|5|sum_discountpercent_sales|[sum_discountpercent_sales](#sum_discountpercent_sales)|Int64(19,notnull)|sum|
|6|sum_spp_sales|[sum_spp_sales](#sum_spp_sales)|Float64(22,notnull)|sum|
|7|sum_forpay_sales|[sum_forpay_sales](#sum_forpay_sales)|Float64(22,notnull)|sum|
|8|sum_finishedprice_sales|[sum_finishedprice_sales](#sum_finishedprice_sales)|Float64(22,notnull)|sum|
|9|sum_pricewithdisc_sales|[sum_pricewithdisc_sales](#sum_pricewithdisc_sales)|Float64(22,notnull)|sum|

### mp_db.stock_size
**Родительская таблица** - [mp_db.stocks_stat](#mp_db.stocks_stat)\
**Присоединяемые таблицы** - нет\
**Группировка по полям** - нет\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|warehouseName|[warehouseName](#warehouseName)|Int32(10,notnull)|-|
|2|nmId|[nmId](#nmId)|String(notnull)|-|
|3|techSize|[techSize](#techSize)|Int32(10,notnull)|-|
|4|quantity|[quantity](#quantity)|String(notnull)|-|

### mp_db.stocks_stat_new
**Родительская таблица** - [mp_db.sales_sta](#mp_db.sales_stat)t\
**Присоединяемые таблицы** - инер джоин [mp_db.stocks_stat](#mp_db.stocks_stat) \
(s.nmId = st.nmId) AND (s.warehouseName = st.warehouseName)\
левый джоин cr - ([mp_db.orders_stat](#mp_db.orders_stat) + [mp_db.sales_stat](#mp_db.sales_stat))\
(cr.nmId = s.nmId) AND (cr.warehouseName = s.warehouseName) AND (cr.date = toDate(s.date)) AND (cr.supplierArticle = s.supplierArticle)\
**Группировка по полям** - s.date, s.warehouseName, s.nmId, s.supplierArticle, cr.totalOrders, cr.totalSales\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|Дата|[Дата](#Дата)|Nullable(10,null)|-|
|2|Склад|[Склад](#Склад)|Nullable(null)|-|
|3|s.nmId|[s.nmId](#s.nmId)|Nullable(10,null)|-|
|4|Количество Продаж Всего|[Количество Продаж Всего](#Количество Продаж Всего)|Nullable(20,null)|count|
|5|Сумма Продаж По PriceWithDisc|[Сумма Продаж По PriceWithDisc](#Сумма Продаж По PriceWithDisc)|Nullable(22,null)|sum|
|6|Количество Остатков|[Количество Остатков](#Количество Остатков)|Nullable(10,null)|max|
|7|Количество Товаров В Пути К Клиент|[Количество Товаров В Пути К Клиент](#Количество Товаров В Пути К Клиент)|Nullable(10,null)|max|
|8|s.supplierArticle|[s.supplierArticle](#s.supplierArticle)|Nullable(null)|-|
|9|Общее Количество Заказов|[Общее Количество Заказов](#Общее Количество Заказов)|Nullable(20,null)|-|
|10|Общее Количество Продаж|[Общее Количество Продаж](#Общее Количество Продаж)|Nullable(20,null)|-|

### mp_db.unitka
**Родительская таблица** - [mp_db.sales_detail_report_summary](#mp_db.sales_detail_report_summary)\
**Присоединяемые таблицы** - полный джоин [mp_db.ads_stat_summary](#mp_db.ads_stat_summary\)\
(sdrs.Дата продажи = ass.date_ads) AND (sdrs.Артикул ВБ = ass.nmid_ads)\
 полный джоин [mp_db.paid_storage_summary](#mp_db.paid_storage_summary)\
(sdrs.Дата продажи = pss.date) AND (sdrs.Артикул ВБ = pss.nmId)\
 полный джоин [mp_db.cost_price](#mp_db.cost_price)\
(cp.nmID = sdrs.Артикул ВБ)\
 полный джоин [mp_db.sales_stat_summary](#mp_db.sales_stat_summary)\
(sss.nmid_sales = sdrs.Артикул ВБ) AND (sdrs.Дата продажи = sss.date_sales)\
**Группировка по полям** - нет\
**Дополнительные условия** - нет

|Номер столбца|Название столбца|Ссылка на родительский столбец|Тип столбца|Агрегация|
|:---:|:---:|:---:|:---:|:---:|
|1|sdrs.Артикул ВБ|[sdrs.Артикул ВБ](#sdrs.Артикул ВБ)|Nullable(10,null)|-|
|2|sdrs.Артикул продовца|[sdrs.Артикул продовца](#sdrs.Артикул продовца)|Nullable(null)|-|
|3|sdrs.Дата продажи|[sdrs.Дата продажи](#sdrs.Дата продажи)|Nullable(10,null)|-|
|4|sdrs.Количество|[sdrs.Количество](#sdrs.Количество)|Nullable(22,null)|-|
|5|sdrs.Цена до скидок|[sdrs.Цена до скидок](#sdrs.Цена до скидок)|Nullable(22,null)|-|
|6|sdrs.Цена (со скидкой продавцадо СПП)|[sdrs.Цена (со скидкой продавцадо СПП)](#sdrs.Цена (со скидкой продавцадо СПП))|Nullable(22,null)|-|
|7|sdrs.Логистика|[sdrs.Логистика](#sdrs.Логистика)|Nullable(22,null)|-|
|8|sdrs.Комиссия ВБ|[sdrs.Комиссия ВБ](#sdrs.Комиссия ВБ)|Nullable(22,null)|-|
|9|sdrs.Штрафы|[sdrs.Штрафы](#sdrs.Штрафы)|Nullable(22,null)|-|
|10|sdrs.Платная премка|[sdrs.Платная премка](#sdrs.Платная премка)|Nullable(22,null)|-|
|11|ass.date_ads|[ass.date_ads](#ass.date_ads)|Nullable(10,null)|-|
|12|ass.nmid_ads|[ass.nmid_ads](#ass.nmid_ads)|Nullable(10,null)|-|
|13|ass.views_ads|[ass.views_ads](#ass.views_ads)|Nullable(19,null)|-|
|14|ass.clicks_ads|[ass.clicks_ads](#ass.clicks_ads)|Nullable(19,null)|-|
|15|ass.sum_ads|[ass.sum_ads](#ass.sum_ads)|Nullable(22,null)|-|
|16|ass.atbs_ads|[ass.atbs_ads](#ass.atbs_ads)|Nullable(19,null)|-|
|17|ass.orders_ads|[ass.orders_ads](#ass.orders_ads)|Nullable(19,null)|-|
|18|ass.shks_ads|[ass.shks_ads](#ass.shks_ads)|Nullable(19,null)|-|
|19|ass.sum_price_ads|[ass.sum_price_ads](#ass.sum_price_ads)|Nullable(22,null)|-|
|20|pss.date|[pss.date](#pss.date)|Nullable(10,null)|-|
|21|pss.nmId|[pss.nmId](#pss.nmId)|Nullable(10,null)|-|
|22|pss.sum_warehousePric|[pss.sum_warehousePric](#pss.sum_warehousePric)|Nullable(22,null)|-|
|23|pss.sum_barcodesCount|[pss.sum_barcodesCount](#pss.sum_barcodesCount)|Nullable(22,null)|-|
|24|cp.nmID|[cp.nmID](#cp.nmID)|Nullable(10,null)|-|
|25|cp.cost|[cp.cost](#cp.cost)|Nullable(22,null)|-|   




