# Condition

Condition - компонент приложения позволяет в удобной форме оформить условие в коде программы и выполнить его.


## Как использовать?

Получить любым удобным способом строитель условий (ConditionBuilder).
Передать на вход метода ConditionBuilder::build() нотацию и получить экземпляр условия.
Воспользоваться экземпляром условия там где требуется его проверка.

```php
$builder = new ConditionBuilder();
$condition = $builder->build($notation);
$condition->execute($model);
```


## Какие условия можно создавать?
- Условие сравнения
- Условие на основе функции обратного вызова
- Хеш условие
- In
- Not
- Between
- Like
- And
- Or


### Условие сравнения

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build([
    '>', 'attribute1', 1
]);
$condition->execute($model);
```

Операторы сравнения

"equal", "=", "not equal", "!=", "more", ">", "more or equal", ">=", "less", "<", "less or equal", "<=".


### Условие на основе функции обратного вызова

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build(function($model){
    return $model->discount > (($model->price + $model->discount) * 0,5);
});
$condition->execute($model);
```


### Хеш условие

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build([
    'attribute1' => ['Foo', 'Bzz'], // На основании этого элемента будет построено IN - условие
    'attribute2' => 'value2'
]);
$condition->execute($model);
```


### IN условие

```php
/** @var ConditionBuilder $builder */
// Формат для записи условия избранный первоначально
$condition = $builder->build([
    'in', [
        'attribute' => ['Foo', 'Bzz']
    ],
]);

// Формат реализованный для соответсвия Yii2
$condition = $builder->build([
    'in', 'attribute', ['Foo', 'Bzz']
]);
$condition->execute($model);
```


### NOT условие

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build([
    'not', [
        '>=', 'attribute1' , 100
    ]
]);
$condition->execute($model);
```


### BETWEEN условие

```php
/** @var ConditionBuilder $builder */
// Формат для записи условия избранный первоначально
$condition = $builder->build([
    'between', [
        'attribute' => [1, 10]
    ],
]);

// Формат реализованный для соответсвия Yii2
$condition = $builder->build([
    'between', [
        'attribute' => [1, 10]
    ],
]);
$condition->execute($model);
```


### LIKE условие

```php
/** @var ConditionBuilder $builder */
// Формат для записи условия избранный первоначально
$condition = $builder->build([
    'like', [
        'attribute' => "/F.o/"
    ],
]);

// Формат реализованный для соответсвия Yii2
$condition = $builder->build([
    'like', 'attribute', "/F.o/"
]);
$condition->execute($model);
```


### AND условие

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build([
    'and', [
        '>=', 'attribute1' , 1
    ], [
        'attribute2' => 'value2'
    ]
]);
$condition->execute($model);
```


### OR условие

```php
/** @var ConditionBuilder $builder */
$condition = $builder->build([
    'or', [
        '>=', 'attribute1' , 1
    ], [
        'attribute2' => 'value2'
    ]
]);
$condition->execute($model);
```

