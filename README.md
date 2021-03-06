# drust-concept

В данном файле описан базовый синтаксис возможного объединения языков программирования D + RUST

## Переменные

Переменные объявляются схожим с Rust образом:

```
let x = 25; // Иммутабельные переменная
let mut y = 23; // Мутабельная переменная

let x: i32 = 23; // иммутабельная переменная с явным указанием типа, тип указывается через точку с запятой
```

Наименования числовых типов взять из Rust(i32, u32, f32 и т.д.), где числом указан размер в битах

## If-Else

If(и остальные подобные конкрукции) могут возвращать выражения и блоки должны быть заключены обязательно в скобки

```
let x = 3;

if x == 3 {
    ...
} else if x == 5 {

} else {

}
```

По умолчанию if возвращает пустое значение(или как правильнее назвать), то есть пустой кортеж.

То есть в полном виде любой if выглядит так:

```
let _: () = if true {
    ()
} else {
    ()
}
```

## Циклы

Тут стоит вопрос, необходим ли `for` в сишном виде или стоит оставить лишь по итератору(как в расте)

```
for i in 0..9 {
    // тело цикла
}
```

Хотелось бы сделать возможность возвращать значения из циклов, но тогда необходимо делать аналог генераторов из c#

```
let x: Iterator<i32> = for i in 0..9 {
    yield i; // необходимо ли для таких случаев вводить слово yield?
}
```

В расте `for` и `while` всегда возвращают пустое значение(надо проверить).


## Структуры и классы

Тут конкретных идей нет, как сделать лучше. Объявление данных и реализацию оставил бы по отдельности, не смешивая
Общая идея для классов на структурах такая:

```
struct Child {
    parent: Parent,
}

impl Parent by self.parent for Child { 
    // тут переопределяются методы базового класса
}
```
Но при таком подходе надо прорабовать как определять, какие реализации трейтов(интерфейсов) подтягивать из родительских классов.
И стоит ли вообще рассматривать такой подход.


## Трейты(интерфейсы)

Трейты бы я полностью перенес из раста, так как они более мощнее интерфейсов и при этом не повышают нагрузку на разработчика.


## Шаблоны

Шаблоны стоит перенять из Ди с некоторыми ограничениями: запретить ограничение входных параметров каким шаблоном, оставить только проверку на реализацию трейта. Убрать результирующий тип auto, ибо он не говорит нам о том, что вернут.

```
fn foo<T>(obj: T) {
    for field in Type::<T>::fields() {
        println(field.name)
    }
} 
```

Очень грубый пример перебора доступных в данной области видимости полей объекта и вывод их имен.

Ключевые слова `impl` и `dyn` для параметров и возвращаемого типа из раста под вопросом. Может стоит сделать как-то проще?