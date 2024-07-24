  # Основная техническая информация
хост:порт 77.232.130.241:8123\
login: admin\
password: 12345m678\
Схемы:
* default - пустая
* mp_db - основная
  
  # 1. Датасеты
Список датасетов:
1. Выкупы;
1. Основной датасет;
1. Остатки;
1. Остатки размеры;
1. План факт;
1. Юнит экономика.
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

### Датасет Выкупы
**Таблица / представление** - [mp_db.kt_stats](#mp_db.kt_stats)\
**Есть ли расчетные поля** - нет\
**Наличие параметров** - нет\
**Фильтрация** - нет


| Номер поля | Поле | Формула | Тип и аггрегация | Ссылка на родительскую таблицу |
| ---------- | ---- | ---- | ---- | ---- |
| 1 | id   | нет | Целое число / нет | [mp_db.kt_stats.id](#mp_db.kt_stats) |
| 2 | nmID | нет | Целое число / нет | [mp_db.kt_stats.nmID](#mp_db.kt_stats) |
| 3 | imtName   | нет | Строка / нет | [mp_db.kt_stats.imtName](#mp_db.kt_stats) |
| 4 | vendorCode   | нет | Строка / нет | [mp_db.kt_stats.vendorCode](#mp_db.kt_stats) |
| 5 | dt   | нет | дата и время / нет | [mp_db.kt_stats.dt](#mp_db.kt_stats) |
| 6 | openCardCount   | нет | Целое число / нет | [mp_db.kt_stats.openCardCount](#mp_db.kt_stats) |
| 7 | addToCartCount   | нет | Целое число / нет | [mp_db.kt_stats.addToCartCount](#mp_db.kt_stats) |
| 8 | ordersCount   | нет | Целое число / нет | [mp_db.kt_stats.ordersCount](#mp_db.kt_stats) |
| 9 | ordersSumRub   | нет | Дробное число / нет | [mp_db.kt_stats.ordersSumRub](#mp_db.kt_stats) |
| 10 | buyoutsCount   | нет | Целое число / нет | [mp_db.kt_stats.buyoutsCount](#mp_db.kt_stats) |
| 11 | buyoutsSumRub   | нет | Дробное число / нет | [mp_db.kt_stats.buyoutsSumRub](#mp_db.kt_stats) |
| 12 | buyoutPercent   | нет | Дробное число / нет | [mp_db.kt_stats.buyoutPercent](#mp_db.kt_stats) |
| 13 | addToCartConversion   | нет | Дробное число / нет | [mp_db.kt_stats.addToCartConversion](#mp_db.kt_stats) |
| 14 | cartToOrderConversion   | нет | Дробное число / нет | [mp_db.kt_stats.cartToOrderConversion](#mp_db.kt_stats) |





# Database Tables Documentation

## mp_db.advert_stats

| Номер столбца | Название столбца | Тип столбца            | Описание                                                                                                      |
|---------------|------------------|------------------------|---------------------------------------------------------------------------------------------------------------|
| 1             | id               | Int32(10,notnull)      | Идентификатор записи                                                                                          |
| 2             | date             | DateTime(29,notnull)   | Даты, за которые необходимо выдать информацию.                                                                |
| 3             | advertId         | Int32(10,notnull)      | ID кампании                                                                                                    |
| 4             | appType          | Int32(10,notnull)      | не нашел                                                                                                       |
| 5             | nmId             | Int32(10,notnull)      | Артикул Wildberries                                                                                           |
| 6             | views            | Int32(10,notnull)      | Количество просмотров. За все дни, по всем артикулам WB и платформам.                                          |
| 7             | clicks           | Int32(10,notnull)      | Количество кликов. За все дни, по всем артикулам WB и платформам.                                              |
| 8             | sum              | Float32(12,notnull)    | Затраты, ₽. За все дни, по всем артикулам WB и платформам.                                                     |
| 9             | atbs             | Int32(10,notnull)      | Количество добавлений товаров в корзину. За все дни, по всем артикулам WB и платформам.                        |
| 10            | orders           | Int32(10,notnull)      | Количество заказов. За все дни, по всем артикулам WB и платформам.                                             |
| 11            | shks             | Int32(10,notnull)      | Количество заказанных товаров, шт. За все дни, по всем артикулам WB и платформам.                              |
| 12            | sum_price        | Float32(12,notnull)    | Заказов на сумму, ₽ За все дни, по всем артикулам WB и платформам.                                             |
| 13            | ctr              | Float32(12,notnull)    | Показатель кликабельности. Отношение числа кликов к количеству показов. Выражается в процентах.                 |
| 14            | cpc              | Float32(12,notnull)    | Средняя стоимость клика, ₽. За все дни, по всем артикулам WB и платформам.                                      |
| 15            | cr               | Float32(12,notnull)    | CR(conversion rate) — это отношение количества заказов к общему количеству посещений кампании.                  |
| 16            | name             | String(notnull)        | Предмет                                                                                                        |

## mp_db.ads_stat_summary

**Родительская таблица:** [mp_db.advert_stats](#mp_dbadvert_stats)  
**Присоединяемые таблицы:** нет  
**Группировка по полям:** date_ads, nmId

| Номер столбца | Название столбца | Тип столбца      | Агрегация | Ссылка на родительскую таблицу  |
|---------------|------------------|------------------|-----------|---------------------------------|
| 1             | date_ads         | Date(10,notnull) | -         | [date](#mp_dbadvert_stats)      |
| 2             | nmid_ads         | Int32(10,notnull)| -         | [nmId](#mp_dbadvert_stats)      |
| 3             | views_ads        | Int64(19,notnull)| sum       | [views](#mp_dbadvert_stats)     |
| 4             | clicks_ads       | Int64(19,notnull)| sum       | [clicks](#mp_dbadvert_stats)    |
| 5             | sum_ads          | Float64(22,notnull)| sum     | [sum](#mp_dbadvert_stats)       |
| 6             | atbs_ads         | Int64(19,notnull)| sum       | [atbs](#mp_dbadvert_stats)      |
| 7             | orders_ads       | Int64(19,notnull)| sum       | [orders](#mp_dbadvert_stats)    |
| 8             | shks_ads         | Int64(19,notnull)| sum       | [shks](#mp_dbadvert_stats)      |
| 9             | sum_price_ads    | Float64(22,notnull)| sum     | [sum_price](#mp_dbadvert_stats) |
