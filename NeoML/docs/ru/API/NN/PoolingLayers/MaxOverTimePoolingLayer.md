# Класс CMaxOverTimePoolingLayer

<!-- TOC -->

- [Класс CMaxOverTimePoolingLayer](#класс-cmaxovertimepoolinglayer)
    - [Настройки](#настройки)
        - [Размер фильтра](#размер-фильтра)
        - [Шаг фильтра](#шаг-фильтра)
    - [Обучаемые параметры](#обучаемые-параметры)
    - [Входы](#входы)
    - [Выходы](#выходы)

<!-- /TOC -->

Класс реализует слой, выполняющий `Max Pooling` над набором последовательностей объектов, с фильтром вдоль оси `BatchLength`.

## Настройки

### Размер фильтра

```c++
void SetFilterLength(int length);
```

Длина фильтра. Если задать равной `0` или отрицательным, то слой будет брать максимум вдоль всей оси.

### Шаг фильтра

```c++
void SetStrideLength(int length);
```

Шаг фильтра в тех случаях, когда размер фильтра положительный.

## Обучаемые параметры

Слой не имеет обучаемых параметров.

## Входы

На единственный вход подается [блоб](../DnnBlob.md) с набором последовательностей:

- `BatchLength` - длина последовательности;
- `BatchWidth * ListSize` - количество последовательностей;
- `Height * Width * Depth * Channels` - размер векторов в последовательностях.

## Выходы

Единственный выход содержит блоб с результатами.

Если `GetFilterLength()` положителен, то `BatchLength` блоба с результатами равен  
`(BatchLength - GetFilterLength()) / GetStrideLength() + 1`.

Если `GetFilterLength()` равен `0` или отрицателен, то `BatchLength` блоба с результатами равен `1`.

Остальные размеры блоба выхода равны соответствующим размерам входа.
