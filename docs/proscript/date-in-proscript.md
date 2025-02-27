---
sidebar_position: 7
sidebar_label: 'Обработка даты'
---

# Обработка даты в PROScript

В шаблоне письма можно работать как с текущей датой, так и с датой, переданной из анкетных данных получателя письма.

По умолчанию при отсутствующем шаблоне форматирования даты мы пытаемся нормализовать входную строку в необходимый для работы формат даты и времени.

Временная зона по умолчанию — Europe/Moscow

## datetime()

Получение из строки объекта типа датавремя:

```
[% dt = datetime('2008-05-30 00:00:00','pattern' => '....', 'time_zone' => ...., ......) %]
```

## datetime_now()

Получаем текущую дату:

```
[% dt = datetime_now('time_zone' => ...., ......) %]
```

## date.format()

Форматируем дату в нужный формат

```
[% d = date.format(datetime_now(),"%m%d","en_EN.UTF-8") %]
```

если надо взять дату из анкеты:

```
[% dt = datetime(anketa.foo.bar)%]
[% dt = date.format(dt,"%m%d","en_EN.UTF-8") %]
```

## Шаблоны форматирования даты

```
%a — день недели (сокр.)
%A — день недели
%b — месяц (сокр.)
%B — месяц
%c — ctime формат: Thu 22 Feb 2024 04:15:21 PM MSK
%d — день месяца с ведущими нулями (01..31)
%e — день месяца, но без ведущих нулей
%D — MM/DD/YY
%G — номер недели GPS (кол-во недель с 6 января 1980)
%h — тоже самое, что и %b
%H, %k — час, 24-часовая система, ведущие нули
%I, %l — час, 12-часовая система, ведущие нули
%j — день года c ведущими нулями
%m —  номер месяца с ведущими нулями
%M — минута с ведущими нулями
%p — AM или PM
%P  — am или pm
%r, %X — время в формате: 09:05:57 PM
%R —  время в формате: 21:05
%s — секунд с начала Эпохи (компьютерное время, начиная с 00:00:00 1 января 1970 г.)
%S — секунд, ведущие нули
%T — время в формате: 21:05:57
%U — номер недели в году (воскресенье первый день недели)
%w — номер дня недели, Воскресенье == 0
%W — номер недели в году (понедельник первый день недели)
%x —  дата в формате: 02/22/2024
%y — год (2 символа)
%Y — год (4 символа)
%Z — временная зона в символах, напр. MSK
```

## Изменение даты перед использованием

Иногда нужно вывести не конкретную дату, а ее измененное значение. Для этого вы можете добавить к имеющейся дате необходимые периоды времени:

```
[% date.format(datetime_now().add("years","+7")) %]
[% date.format(datetime_now().add("months","+7")) %]
[% date.format(datetime_now().add("days","+7")) %]
[% date.format(datetime_now().add("hours","+7")) %]
[% date.format(datetime_now().add("minutes","+7")) %]
[% date.format(datetime_now().add("seconds","+7")) %]
```

Чтобы отнять период:

```
[% date.format(datetime_now().add("days","-7")) %]
```

Использовать дату выпуска, как базовую дату:

```
[% date.format(datetime(param.issue.dt).add("days","+7"),"%d.%m.%Y") %]
```

Использовать анкетные данные, как базовую дату:

```
[% date.format(datetime(anketa.a917.q904).add("days","+7"),"%d.%m.%Y") %]
```

## format_datetime_duration(dta,dtb)

Иногда требуется сравнить две даты и получить интервал.

```
[% format_datetime_duration(dta,dtb) %]

[% format_datetime_duration(dta,dtb,"format":"FMT") %]
```

Перед вами могу стоять две задачи: просто посчитать интервал с нужной точностью или вывести полученный интервал с желаемым форматированием.

Вначале разберёмся с форматированием результата сравнения.

В примерах использованы значения

```
[% dta = "2018-02-26T15:13:00" %]
[% dtb = "2018-02-05 12:11:58" %] <---- наличие T без разницы
```

Форматирование задается в в параметре **format** и может быть двух типов:

_строка_ — один из предустановленых форматов описанных ниже

_массив_ — от одного до четырёх элементов задающих, что приписать справа после компоненты времени

длительность в секундах

```
[ s ]
```

длительность в секундах и минутах

```
[ m, s ]
```

длительность в секундах, минутах и часах

```
[ h, m, s ]
```

длительность в секундах, минутах, часах и днях

```
[ D, h, m, s ]
```

Если элемент есть, но не определён, то соответствующий компонент не выводится:

длительность в минутах, часах и днях

```
[ D, h, m, undef ]
```

Первый выводимый компонент идёт без лидирующего нуля, остальные — с лидирующим нулём.

Если элемент не строка, а массив, то включается учёт множественного числа, а массив должен содержать формы слова для одного, двух и пяти компонентов времени.

На примерах рассмотрим, как всё работает.

## Формат отсутствует

На самом деле действует следующий формат:

```
 [' ',':',':','']
21 03:01:02
```

## Склоняем полученный результат

```
'plural_Ds' => [[" день "," дня "," дней "],[" час "," часа "," часов "],[" минута "," минуты "," минут "],[" секунда "," секунды ","секунд"]]

'plural_Dm' => [[" день "," дня "," дней "],[" час "," часа "," часов "],[" минута "," минуты "," минут "],undef]

'plural_Dh' => [[" день "," дня "," дней "],[" час "," часа "," часов "],undef,undef]

'plural_hs' => [[" час "," часа "," часов "],[" минута "," минуты "," минут "],[" секунда "," секунды "," секунд"]]

'plural_hm' => [[" час "," часа "," часов "],[" минута "," минуты "," минут "],undef]
```

```
[% format_datetime_duration(dta,dtb,"format","plural_Ds") %]

21 день 03 часа 01 минута 02 секунды
```

```
[% format_datetime_duration(dta,dtb,"format","plural_hm") %]

507 часов 01 минута
```

## Выводим аббревиатуры вместо полных слов

```
'abbr_Ds' => [ ' д ',' ч ',' м ',' c' ]
'abbr_Dm' => [ ' д ',' ч ',' м ',undef]
'abbr_Dh' => [ ' д ',' ч ',undef,undef]
'abbr_hs' => [       ' ч ',' м ',' c' ]
'abbr_hm' => [       ' ч ',' м ',undef]
```

```
[% format_datetime_duration(dta,dtb,"format","abbr_Dh") %]

21 д 03 ч
```

## Выводим аббревиатуры слитно с числами

```
'abbr_tog_Ds' => [ 'д ','ч ','м ' ,'c'  ]
'abbr_tog_Dm' => [ 'д ','ч ','м ' ,undef]
'abbr_tog_Dh' => [ 'д ','ч ',undef,undef]
'abbr_tog_hs' => [      'ч ','м ' ,'c'  ]
'abbr_tog_hm' => [      'ч ','м ' ,undef]
```

```
[% format_datetime_duration(dta,dtb,"format","abbr_tog_Dh") %]

21д 03ч
```

А теперь переходим к определению интервала с нужной точностью. Для этого нам надо привести в нужный формат исходные даты и вывести интервал с нужным форматированием.

## Определяем разницу в днях

```
[% today = date.format(datetime_now(),"%Y-%m-%d","en_EN.UTF-8") %]

[% period = format_datetime_duration(suspend_date,today,"format", ['',undef,undef,undef]) %]

[% IF period == 3 %]срок три дня [% END %]
```
