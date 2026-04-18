# Управленческая отчётность по Northwind (BI-дашборды) 📊

---

<img src="https://github.com/microsoft/PowerBI-Icons/blob/main/SVG/Power-BI.svg" width="20"/> ![Static Badge](https://img.shields.io/badge/POWER%20BI-yellow?style=for-the-badge) <img src="https://github.com/devicons/devicon/blob/master/icons/mysql/mysql-original.svg" height="28"/> ![Static Badge](https://img.shields.io/badge/MySQL-blue?style=for-the-badge) ![Static Badge](https://img.shields.io/badge/DATASET-Northwind-lightblue?style=for-the-badge)

---

## **Содержание** 📋
- [Описание работы](#описание-работы-)
- [Модель данных](#модель-данных-)
- [Предобраюотка данных](#предобработка-данных-)
- [Превью дашбордов](#превью-дашбордов-%EF%B8%8F)
- [Цели и задачи дашбордов](#цели-и-задачи-дашбордов-)

---

## **Описание работы** 📜

На основе учебного набора данных **Northwind** предоставленного _Microsoft_ мной были разработаны дашборды, позволяющие принимать различные решения в соответствие с аналитикой по продажам, по эффективности персонала и по логистике.

---

## **Модель данных** 🔗

В датасете присутствует несколько ключевых таблиц, связанных между собой по схеме **Звезда**

<img src="https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Model_of_data.png" height="600"/>

В модель Northwind входят:
- `orders` - Записи о заказах
- `order_details` - Детали  каждого заказа (скидка, количество, цена)
- `employees` - Данные о сотрудниках (ФИО, город, контакты, отдел, должность)
- `customers` - Данные о покупателях (ФИО, город, компания, контакты)
- `shippers` - Данные о поставщиках (компания, контакты, адрес)

_Дополнительно:_ мной был создан автоматический календарь который написан на языке DAX. Он автоматически вычисляет все даты, которые присутствуют в файле и формирует новый календарь. ❗После создания с ним необходимо настроить связи.
```
Dates (Auto) = 
ADDCOLUMNS (
    CALENDARAUTO(12),
    "Year", YEAR([Date]),
    "MonthNo", MONTH([Date]),
    "MonthName", FORMAT([Date], "[$-ru-RU]MMMM"),
    "YearMonth", FORMAT([Date], "YYYY-MM"),
    "Quarter", "Q" & FORMAT ( [Date], "Q" ),
    "DayOfWeekNo", WEEKDAY([Date], 2),
    "DayOfWeekName", FORMAT([Date], "[$-ru-RU]dddd")
)
```

---

## **Предобработка данных** 👔

1) *Загрузка данных* ⏬ : Загрузка происходила через MySQL сервер, размещённый на университетском сервере.

3) *Автоматический календарь* 🗓️:  Как было сказано выше, для анализа динамики по временным интервалам был создан автоматический календарь.

5) *Исправление дат* ❌: Автоматический календарь создаёт даты со временем `00:00:00`, а в некоторых записях время отличалось. Для решения проблемы нужно было загрузить запрос к данным в редакторе **PowerQuery**, где столбец с датой и временем разделялось, создавался новый столбец, а после столбцы заново соединялись.

7) *ФИО Сотрудников* 👩‍💼👨‍💼: `ФИО сотрудника = 'northwind employees'[last_name] & " " & 'northwind employees'[first_name]`

9) *ФИО Клиентов* 🛒: `ФИО клиента = 'northwind customers'[last_name] & " " & 'northwind customers'[first_name]`

---

## **Превью дашбордов** 🖼️

| **Анализ по продажам** | **Анализ по сотрудникам** | **Анализ по логистике** |
| :---: | :---: | :---: |
| ![Sells](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/screenshots/orders_for_clients.png) | ![Employees](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/screenshots/orders_for_managers.png) | ![Logistics](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/screenshots/orders_for_logistics.png) |
| [Orders_for_clients.pbix](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Orders_for_clients.pbix) |[Orders_for_managers.pbix](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Orders_for_managers.pbix) | [Logistics.pbix](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Logistics.pbix) |
| [Orders_for_clients.pdf](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Orders_for_clients.pdf) |[Orders_for_managers.pdf](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Orders_for_managers.pdf) | [Logistics.pdf](https://github.com/m0zerrr/PowerBi-dashboards/blob/main/Logistics.pdf) |

---

## **Цели и задачи дашбордов** 📌

### ***Для отдела продаж*** 🛍️
* 🔢 **Ключевые метрики:** `Средний доход на клиента`, `Средний чек`, `Сегментация по чеку`
* 📰 **Инсайты:** Более ***56%*** клиентов принадлежат к самому высокому сегменту по величине среднего чека (`5000+ долларов`). Двумя лидерами по среднему чеку, значение которого превышает ***2 тыс. долларов***, являются `Xie Ming-Yang` и `Raghav Amritansh`.

### ***Для менеджмента*** 🎯
* 🔢 **Ключевые метрики:** `Сумма заказов`, `Средний чек`, `Плотность нагрузки по дням недели`
* 📰 **Инсайты:** Наибольшую часть прибыли с продаж в общую сумму дохода привнёс `Freehafer Nancy`, однако по производительности лидирует `Hellung-Larsen Anne`. Средний чек на сотрудника составил ***1,42 тыс. долларов***. Если оценивать по стабильности, то `Setgienko Mariya` работает равномерно в каждый свой рабочий день.

### ***Для логистики*** 🚚
* 🔢 **Ключевые метрики:** `Среднее время доставки`, `Топ проблемных городов`, `Сезонность`
* 📰 **Инсайты:** Среднее время доставки в марте составляет менее 1 дня. Города **Chicago**, **Las Vegas** и **Los Angelas** входят в топ 3 проблемных городов. В марте среднее время доставки до _Chicago_ удерживалось на отметке **7 дней**, что является критическмм значением. Опоздало при этом за всё время всего ***2%*** заказов.
