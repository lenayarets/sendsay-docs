---
sidebar_position: 4
sidebar_label: 'Экспорт данных и контактов'
---

# Как экспортировать контакты в новом интерфейсе

:::tip Важно
Если вы хотите экспортировать не только контакты, но и другие данные подписчиков, это можно сделать [в предыдущем интерфейсе](https://sendsay.ru/account/#dashboard).

[Как экспортировать контакты и данные подписчиков](https://docs.sendsay.ru/subscribers/import-and-export/how-to-export-data-in-the-legacy-interface#как-экспортировать-данные-подписчиков)
:::

## Как экспортировать контакты из списка или сегмента

1. Откройте список или сегмент. В правом верхнем углу страницы откройте выпадающий список и выберите «Экспортировать как XLSX» или «Экспортировать как CSV».
2. Зайдите в журнал заданий — там появилось задание на экспорт выбранного списка или сегмента. Откройте выпадающее меню напротив него и выберите «Загрузить».

![How to export contacts from list](/img/subscribers/import-and-export\how-to-export-contacts-in-the-new-interface/how-to-export-contacts-from-list.png) <br/>

## Как экспортировать все контакты одного типа

1. Зайдите в раздел **Подписчики → Сегменты**, создайте сегмент и выберите тип контактов, который вы хотите экспортировать (email, веб-пуш, смс или CSID).
2. В новом сегменте перейдите во вкладку **Настройка условий**. Чтобы отобрать всех подписчиков с нужным контактом, на новой строке нажмите на плюсик и поставьте следующие значения:
   - вместо «состоит в группе» — «имеет данные»,
   - в поле для ключа — пункт «OBJ Системная», подпункт «ID подписчика»,
   - в поле для условия — «Заполнено».
3. Нажмите «Сохранить».
4. В правом верхнем углу откройте выпадающий список и нажмите на «Экспортировать как XLSX» или «Экспортировать как CSV».
