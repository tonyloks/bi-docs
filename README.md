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
| 1 | Последняя выгруженная дата | ``` max([Дата] BEFORE FILTER BY [Дата]) ``` | авто | нет |
| 2 | ДРР от продаж до спп   | ``` if [Выкупили на сумму, руб. (КТ)]!= 0 then [Расход, руб. (Р)] / [Выкупили на сумму, руб. (КТ)] else NULL end ``` | авто | нет |
| 3 |  ДРР от заказов до спп  | ``` if [Заказали на сумму, руб. (КТ)] != 0     then [Расход, руб. (Р)] / [Заказали на сумму, руб. (КТ)] else    NULL end ```  | авто | нет |
| 4 |  Артикул продавца  | ``` art.supplierArticle ```  | нет | нет |
| 5 |  Продажи  | ``` if [selected_measure] = 'Количество'     then [Количество продаж, шт. (П)] ELSE [Цена со скидкой продавца, руб. (П)] end ```  | авто | нет |
| 6 | Заказы   | ``` if [selected_measure] = 'Количество'    then [Количество заказов, шт. (З)] ELSE [Цена со скидкой продавца, руб. (З)] end ```  | авто | нет |
| 7 |  CPC, руб.  | ``` IF [Клики (Р)] != 0    THEN [Расход, руб. (Р)]/[Клики (Р)] ELSE NULL END ```  | авто | нет |
| 8 |  CR из перехода в заказ, %  | ``` if [Переходы в карточку (КТ)] != 0   then [Заказали товаров, шт. (КТ)]/ [Переходы в карточку (КТ)] else NULL end ```  | авто | нет |
| 9 |  Продаж в день  | ``` sum([Количество продаж, шт. (П)]) / [Всего дней в датасете] ```  | авто | нет |
| 10 | Заказов в день   | ``` sum([Заказали товаров, шт. (КТ)]) / [Всего дней в датасете] ```  | авто | нет |
| 11 | Всего дней в датасете   | ``` ([Максимальная дата в датасете]-[Минимальная дата в датасете]) + 1 ```  | авто | нет |
| 12 |  Максимальная дата в датасете  | ``` if max([Дата]) is null then NULL ELSE max([Дата]) end  ```  | авто | нет |
| 13 | Минимальная дата в датасете   | ``` if min([Дата]) is null then NULL ELSE min([Дата]) end ```  | авто | нет |
| 14 |  ДРР рекламы | ``` if [Сумма заказов, руб. (Р)] != 0     then [Расход, руб. (Р)] / [Сумма заказов, руб. (Р)] else     NULL end ```  | авто | нет |
| 15 |  ДРР аккаунта | ```  if [Заказали на сумму, руб. (КТ)] != 0     then [Расход, руб. (Р)] / [Заказали на сумму, руб. (КТ)] else     NULL end  ```  | авто | нет |
| 16 | Карточка товара   | ``` URL('https://www.wildberries.ru/catalog/'+ str([ID карточки]) + '/detail.aspx', str([ID карточки])) ```  | нет | нет |
| 17 |  CR в заказ, % | ``` if [Переходы в карточку (КТ)] != 0     then [Заказали товаров, шт. (КТ)] / [Переходы в карточку (КТ)] else NULL end ```  | авто | нет |
| 18 |  Ср. чек, руб. | ``` IF  [Цена со скидкой продавца, руб. (З)] != 0    THEN [Цена со скидкой продавца, руб. (З)]/[Количество продаж, шт. (П)] ELSE NULL END ```  | авто | нет |
| 19 |  CPO, руб.  | ``` IF [Количество заказов, шт. (Р)] != 0     THEN [Сумма заказов, руб. (Р)]/[Количество заказов, шт. (Р)] ELSE NULL END  ```  | авто | нет |
| 20 |  CTR, %  | ``` IF [Показы (Р)] != 0   THEN [Клики (Р)]/[Показы (Р)] ELSE NULL END ```  | авто | нет |
| 21 |  Скалированная дата | ``` IF [scale_date] = 'День'     then [Дата] ELSEIF [scale_date] = 'Неделя'     then DATETRUNC([Дата],'week') ELSEIF [scale_date] = 'Месяц'     then DATETRUNC([Дата],'month') ELSEIF [scale_date] = 'Квартал'     then DATETRUNC([Дата],'quarter') ELSEIF [scale_date] = 'Год'     then DATETRUNC([Дата],'year') END  ```  | нет | нет |
| 22 |   Выкуп, % | ``` if [Заказали товаров, шт. (КТ)] != 0     then sum([Выкупили товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) / sum([Заказали товаров, шт. (КТ)] BEFORE FILTER BY [Дата]) else   NULL     end ```  | авто | нет |
| 23 |   art.supplierArticle | нет | нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 24 |  ID карточки  | нет | нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 25 |  Дата  | нет | нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 26 |  Название товара  | нет | нет | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 27 |   Переходы в карточку (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 28 |   Положили в корзину (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 29 |   Заказали товаров, шт. (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 30 |   Заказали на сумму, руб. (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 31 |   Выкупили товаров, шт. (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 32 |   Выкупили на сумму, руб. (КТ) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 33 |   Количество заказов, шт. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 34 |   Отмененный закаказов, шт. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 35 |   Выкупленных заказов, шт. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 36 |   Сумма заказов, руб. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 37 |   Фактическая цена, руб. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 38 |   Цена со скидкой продавца, руб. (З) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 39 |   Количество продаж, шт. (П) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 40 |   Сумма продаж, руб. (П) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 41 |   К перечислению, руб. (П) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 42 |   Фактическая цена, руб. (П) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 43 |   Цена со скидкой продавца, руб. (П) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 44 |   Показы (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 45 |   Клики (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 46 |   Расход, руб. (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 47 |   Положили в корзину, шт. (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 48 |   Количество заказов, шт. (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 49 |   Кол-во заказанных товаров, шт. (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |
| 50 |   Сумма заказов, руб. (Р) | нет | сумма | [mp_db.nmid_fullstat_renamed](#mp_db.nmid_fullstat_renamed) |

### Остатки
**Таблица / представление** - [mp_db.stocks_stat_new](#mp_db.stocks_stat_new)\
**Есть ли расчетные поля** - да\
**Наличие параметров** - нет\
**Фильтрация** - нет

| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | if [Всего дней в датасете] > 0thensum([Продажи, шт.]) / [Всего дней в датасете]ELSE NULLend | ``` if [Всего дней в датасете] > 0 then sum([Продажи, шт.]) / [Всего дней в датасете] ELSE NULL end ``` | авто | нет |
| 2 | Продажи Ср./День, шт.   | ``` if [Всего дней в датасете] > 0 then sum([Продажи, шт.]) / [Всего дней в датасете] ELSE NULL end ``` | авто | нет |
| 3 |  На сколько дней хватит, продажи  | ``` if [Продажи Ср./День, шт.] > 0    then [Остатки, шт.] / [Продажи Ср./День, шт.] else NULL     ENd ```  | авто | нет |
| 4 |  Дата последней продажи  | ``` max(max([Дата] INCLUDE [Дата],[nmId],[Склад]) EXCLUDE [Дата]) ```  | нет | нет |
| 5 |  Дней без продаж, дни  | ``` date(now()) - [Дата последней продажи] ```  | авто | нет |
| 6 | ID карточки товара   | ```URL('https://www.wildberries.ru/catalog/'+ str([s.nmId]) + '/detail.aspx', str([s.nmId]))```  | нет | нет |
| 7 |  Ср. чек, руб.  | ```if [Продажи, шт.] > 0 then [Сумма продаж, руб.] / [Продажи, шт.] else NULL end  ```  | авто | нет |
| 8 |  Стоимость остатка, руб.  | ``` [Ср. чек, руб.] * [Остатки, шт.] ```  | авто | нет |
| 9 |  На сколько дней хватит, заказы  | ``` if [Заказов Ср./День, шт.] > 0    then [Остатки, шт.] / [Заказов Ср./День, шт.] else NULL   ENd ```  | авто | нет |
| 10 | Заказов Ср./День, шт.   | ``` if [Всего дней в датасете] > 0 then sum([Общее Количество Заказов]) / [Всего дней в датасете] ELSE NULL end  ```  | авто | нет |
| 11 | Сумма 1 дня простоя, руб.   | ``` if [Всего дней в датасете] > 0 then [Сумма продаж, руб.] / [Всего дней в датасете]  else NULL end  ```  | авто | нет |
| 12 | Минимальная дата в датасете | ``` if min([Дата]) is null then NULL ELSE min([Дата]) end  ```  | авто | нет |
| 13 | Максимальная дата в датасете | ``` if max([Дата]) is null then NULL ELSE max([Дата]) end  ```  | авто | нет |
| 14 |  Всего дней в датасете | ```([Максимальная дата в датасете]-[Минимальная дата в датасете]) + 1```  | авто | нет |
| 15 |  Продажи, шт. | ```[Количество Продаж Всего] ```  | авто | нет |
| 16 | Сумма продаж, руб.   | ``` [Сумма Продаж По PriceWithDisc] ```  | авто | нет |
| 17 |  Остатки, шт.| ```[Количество Остатков] ```  | авто | нет |
| 18 |  Товаров по пути к клиенту, шт. | ```[Количество Товаров В Пути К Клиент] ```  | авто | нет |
| 19 |  Артикул продавца  | ```[s.supplierArticle] ```  | нет | нет |
| 20 | Дата  | нет  | нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 21 | Склад | нет | нет |[mp_db.stocks_stat_new](#mp_db.stocks_stat_new)|
| 22 | s.nmId | нет | нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 23 |  Количество Продаж Всего | нет | сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 24 |  Сумма Продаж По PriceWithDisc  | нет | сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 25 | Количество Остатков  | нет | среднее | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 26 | Количество Товаров В Пути К Клиент | нет | среднее | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 27 | s.supplierArticle | нет | нет | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 28 | Общее Количество Заказов | нет | сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |
| 29 | Общее Количество Продаж | нет | сумма | [mp_db.stocks_stat_new](#mp_db.stocks_stat_new) |








































