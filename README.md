# Goods_Forecast_Hack
## GoodsForecast.OSA – Определение наличия товаров на полке в интервалах без продаж

## Описание кейса
- Система GoodsForecast.OSA анализирует историю продаж в сети магазинов и определяет товары с наибольшей вероятностью отсутствия на полке.
- Сотрудники магазинов по каждой позиции проверяют наличие товара и корректность ценника, при необходимости выставляя продукцию со склада и/или корректируя ценник.
- Таким образом, обеспечивается своевременное обнаружение отсутствия товаров на полке, чтобы покупатели не упустили возможность совершить покупку, а сеть повысила товарооборот.

*OSA (On Shelf Availability) – показатель представленности продукции на полке магазина.*

## Задача
Необходимо решить задачу бинарной классификации – определение наличия товаров на полке в интервалах без продаж с оценкой производительности по метрике AUC-ROC.

**Направление 1** 
Построить модель без использования оценки вероятности отсутствия товара на полке (Probability), представленной в витрине данных.

## Оценка решения
Решение оценивается на основе метрики AUC-ROC на скрытой тестовой выборке.

**Описание данных:**
* `df` - весь дататсет с признаками, признаки зашифрованы
* `train_df` - тренировочная выборка записи из `df` с `IsCorrect` is not null
* `test_df` - тестовая выборка, используется в финальном зачете - записи с `IsCorrect` is null
* `stocks` - датасет с дополнительными данными об остатках
* `sales` - датасет с дополнительными данными о продажах
* `train_checkpoint` - промежуточные результаты выгружаются за следующие даты `ValidationDateTime` >= `2023-07-15`

## Формат выгрузки csv-файла (столбцы):
Для чек-поинтов - это на тренировочных данных, для финального резульата - на тестовых данных
* `LocationId`
* `ProductId`
* `ValidationDateTime`
* `CalculatedProbability` (вычисленная вероятность - `predict_proba()` )

## Описание результата:
- Для реализации задачи обучена модель `CatBoostRegressor`
- Модель предсказывает наличие товара на полке
- Метрика `ROC-AUC` на Чек-поинте №3 = `0.687`

## Команда DS:
* Грибанов Михаил - DS (tl)
* Егоров Михаил - DS
* Якушева Наталья - DS
* Гусев Кирилл - DS
* Азимов Улан - DS
