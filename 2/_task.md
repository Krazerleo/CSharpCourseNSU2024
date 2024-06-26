# Калькулятор Upgrade

Реализовать консольную утилиту, позволяющую проводить операции с
со следующими физическими величинами:

## Физические величины и операторы
---

|Величины                     |Операторы  |
|-----------------------------|-----------|
|Расстояние                   | Сложение  |
|Время                        | Вычитание |
|Скорость                     | Умножение |
|Скалярная величина           | Деление   |
|                             | Скобки    |
---

## Управление работой будет осуществляться следующими коммандами

Работа с командами калькулятора может осуществляться через стандартный поток ввода или через считывания целиком файла с командами на ваш выбор.

|Комманда                           | Обозначения                             
|-----------------------------------|---------------------------------------
|push operator `<operand>`           | `<operator>` из `{+, -, *, /, (, )}`                               
|push value   `<value>`     `<id>`  | `<value>` из `{Speed, Time, Length, Scalar}`
|change value ``<value>``   `<id>`  | Поменять значение по id
|remove value               `<id>`  | Убрать значение из вычислений по id
|compute                            | Вычислить данное выражение, вывести тип и значение

### remove value:
* В случае сложения: ... x + y ... => remove y => ... x + 0 ...
* В случае вычитания: ... x - y ... => remove y => ... x - 0 ...
* В случае умножения: ... x * y ... => remove y => ... x * 1 ...
* В случае деления: ... x / y ... => remove y => ... x / 1 ...
* В случае деления: ... x / y ... => remove x => ... 0 ...
* Существует следующий "порядок" убирания операндов по возрастанию: (+ ; -; *; /)

Примеры:
* F / (A + B * C) => remove F => 0
* (A / B / C) => remove C => A / B
* (A + B * C) => remove B => A + C


## Исключения
* Если выражение после вызова команды compute некорректно, то завершаем программу
с ошибкой, а также указываем, где она произошла.
* Если пытаемся запушить значение не из заданных величин, завершаем программу,
а также показываем список возможных величин (или просто показываем helper)
* Если вставляем значение с повторенным ранее id, или пытаемся удалить значение,
заканчиваем программу с ошибкой.
* Если в ходе выполнения получаем неизвестную величину, то также бросаем исключение.

## Прочие замечания
* Стараемся соблюдать буковку O из SOLID. Не надо жестко привязываться к типу величины.
При добавлении новой физической величины мы не должны сильно модифицировать существующий код. Но можно считать что множество операторов строго зафиксирована, поэтому замечание к этому не относится.
* Подумайте над семантикой исключений. Возможно при использовании неизвестной величины это не вина пользователя, что такой величины нет.
* Если вы чуствуете, что хорошо знаете C#, и при этом не боитесь использовать новые инструменты, то вместо написания велосипедного интерпретатора выражений можете попробовать поработать с LINQ Expressions. За такой подход я могу накинуть 1 балл.