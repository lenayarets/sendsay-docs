---
sidebar_position: 2
sidebar_label: 'Файл для импорта'
---

import fieldCode from "/img/subscribers/import-and-export/how-to-prepare-file-for-import/field-code.png";
import fileForAutoimport from "/img/subscribers/import-and-export/how-to-prepare-file-for-import/file-for-autoimport.png";
import fileForManualImport from "/img/subscribers/import-and-export/how-to-prepare-file-for-import/file-for-manual-import.png";
import listType from "/img/subscribers/import-and-export/how-to-prepare-file-for-import/list-type.png";

# Как подготовить файл для импорта

## 1. Формат файла

Файл должен быть формата csv, txt, xlsx или zip.

## 2. Расположение данных в файле

На одной строке записываются данные одного подписчика, порядок данных в строках должен быть одинаковым. Требования к первой строке файла различаются в зависимости от того, как вы импортируете контакты — вручную или через автоматизацию по времени.

При автоимпорте в первой строке каждого столбца нужно указать код поля, куда будут записаны данные. Код хранится в анкете напротив самого поля, префикс «anketa» копировать не нужно. Например, для столбца с именами нужно скопировать `base.firstName`:

<p align="center">
    <img src={fieldCode} alt="Field code" />
</p>

При автоимпорте у подписчиков может быть только основной контакт (чтобы загружать дополнительные контакты, напишите нам в чат). Весь файл будет выглядеть вот так:

<p align="center">
    <img src={fileForAutoimport} alt="File for autoimport" />
</p>

При обычном импорте через интерфейс коды полей в файле указывать не нужно, так как поля со столбцами сопоставляются вручную. В первой строке файла могут быть указаны наименования столбцов — её можно будет пропустить при импорте.

<p align="center">
    <img src={fileForManualImport} alt="File for manual import" />
</p>

## 3. Разделитель данных

В Excel данные записываются в ячейки таблицы, а в остальных случаях их нужно разделять запятой, точкой с запятой или табуляцией (разделитель должен быть одинаковым в каждой строке).

```csv
pochta1@gmail.com, Иван, Иванов, Москва, 1970-01-21
```

Если у подписчика отсутствуют какие-то данные, вместо них нужно ставить два разделителя подряд (пробелы необязательны).

```csv
pochta2@gmail.com, , Фёдоров, , 1980-02-14
```

## 4. Основной контакт

В файле должен быть один контакт, который заполнен у всех подписчиков (он называется основной контакт). Это может быть:

- электронный адрес,
- телефон,
- идентификатор csid,
- ID пользователя в Телеграме (это комбинация цифр — отправлять рассылки через бота по нику или номеру телефона нельзя).

По основному контакту происходит склеивание данных, если вы загружаете данные, которые уже есть в базе. Подписчики без основного контакта не загружаются. Если вы импортируете контакты в список, тип основного контакта должен совпадать с типом списка:

<p align="center">
    <img src={listType} alt="List type" />
</p>

Если вы импортируете контакты без списка, основной контакт нужно выбрать самостоятельно в настройках импорта:

![How to choose list during import](/img/subscribers/import-and-export\how-to-prepare-file-for-import/how-to-choose-list-during-import.gif) <br/>

## 5. Формат записи дат и телефонных номеров

Даты указываются в формате ГГГГ-ММ-ДД. Например, для даты «1 июля 1993 года» запись будет такой:

```
1993-07-01
```

Телефонные номера можно указывать в любом виде — со скобками, пробелами или цифры подряд. В российских номерах код страны указывать необязательно, а если он есть, то допустим в любом виде — 7, +7 или 8. Номера других стран нужно писать в полном виде.

## 6. Какие данные не загружаются

Чтобы исключить из импорта конкретного подписчика, добавьте символ # в начало строки.

```
#pochta5@gmail.com, Пётр, Петров, Новгород, 1989-01-01
```

В настройках ручного импорта можно указать, какие столбцы не нужно загружать. Также при импорте не загружаются следующие данные:

- контакты с опечатками,
- повторяющиеся контакты (из повторов будет загружен только последний вариант),
- данные, которые не соответствуют формату поля.

:::tip Важно
Страны надо указывать только на русском языке, иначе они не будут загружены
:::

**Читайте также:** [Как настроить параметры импорта](https://docs.sendsay.ru/subscribers/import-and-export/how-to-import-subscribers#2-настройте-параметры-импорта)
