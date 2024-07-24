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
1. mp_db.ads_stat_summary;
1. mp_db.articleadd;
1. mp_db.execute_plan;
1. mp_db.kt_stat_summary;
1. mp_db.nmid_fullstat_renamed;
1. mp_db.order_current;
1. mp_db.orders_stat_summary;
1. mp_db.paid_storage_summary;
1. mp_db.plan_fact_current;
1. mp_db.sales_detail_report_summary;
1. mp_db.sales_stat_summary;
1. mp_db.stock_size;
1. mp_db.stocks_stat_new;
1. mp_db.unitka.
 # 3. Таблицы
Список таблиц:
1. mp_db.ads_cost_history;
1. mp_db.advert_stats;
1. mp_db.cards_content;
1. mp_db.commissions;
1. mp_db.cost_price;
1. mp_db.kt_stats;
1. mp_db.orders_stat;
1. mp_db.paid_storage;
1. mp_db.product_plan;
1. mp_db.sales_detail_report_stat;
1. mp_db.sales_stat;
1. mp_db.stocks_stat.

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





































