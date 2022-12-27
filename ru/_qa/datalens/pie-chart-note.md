### Как сделать подпись с названием сектора и процентом в круговой диаграмме? {#pie-chart-note}

Создайте подпись с помощью вычисляемого поля:

`[<name>] + ' ' + STR(INT(SUM([<value>])/SUM(SUM([<value>]) TOTAL) * 100)) + '%'`

Где:

* `<name>` — поле, по которому будет определяться название сектора;
* `<value>` — поле, значение которого должно отображаться в виде процента.

**Как устроена формула?**

1. Фрагмент `SUM([<value>])/SUM(SUM([<value>]) TOTAL) * 100` вычисляет долю сектора в виде процента.
1. Вычисленное значение округляется функцией [INT](../../datalens/function-ref/INT.md).
1. Значение переводится в строку функцией [STR](../../datalens/function-ref/STR.md) для создания подписей к диаграмме.
1. Название сектора, вычисленное значение и символ `%` объединяются строку оператором сложения `+`.

В качестве альтернативного варианта можно использовать формулу с [LOD-выражением](../../datalens/concepts/lod-aggregation.md#fixed):

`[<name>] + ' ' + STR(INT(SUM([<value>])/SUM([<value>] FIXED) * 100)) + '%'`

Этот вариант дает такой же результат, что и первый. Вы можете попробовать оба и выбрать тот, который эффективнее работает в вашем случае.

**Пример**

Формула: `[Category] + ' ' + STR(INT(SUM([Sales])/SUM(SUM([Sales]) TOTAL) * 100)) + '%'`

См. [изображение](https://storage.yandexcloud.net/doc-files/pie-chart.png).