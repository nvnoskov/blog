+++
date = "2015-08-04T16:51:22+06:00"
draft = false
title = "Сравнение скорости сайтов авиакомпаний и агрегаторов"
slug = "sravnieniie-skorosti-zaghruzki"
image = "/2015/08/image.png"
aliases = [
	"sravnieniie-skorosti-zaghruzki"
]
tags = ["Метеор", "Скорость"]
categories = ["PageSpeed"]
author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++

Увидев в ленте FB [пост](https://www.facebook.com/alimzhan.bissembayev/posts/1134310696582323) о сравнении скорости загрузки сайтов различных авиакомпаний и aviata.kz, решил что отличным продолжением темы ["Скорости загрузки сайтов"](http://blog.vesna.kz/meteor-shop-skorost-pochiemu-ona-vazhna/), будет провести более глубокое исследование на тему клиентской оптимизации, взяв за основу предоставленную выборку, но немного дополнив её.

Сначала поговорим о цифрах, потом разберём каждый сайт отдельно.

Сайты авиакомпаний:

- http://www.bekair.com
- http://www.scat.kz/ru/
- http://airastana.com/kaz/ru-RU

Агрегаторы авиабилетов:

- https://www.chocotravel.com/
- http://aviasales.kz/
- https://aviata.kz/
- https://flight.kz/

## Часть 1. Цифры
Основным (и самым простым) параметром при загрузке страницы является её объём. Он влияет на время загрузки документа (стилей и скриптов) в браузер пользователя.
### Вес страницы (Кб)
Суммарный вес страницы, включая скрипты, стили и изображения. Чем он меньше тем лучше, особенно на мобильных устройствах.
<iframe width="537.7258160773808" height="310.524291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=544889000&amp;format=interactive"></iframe>

### Вес JS-кода (Кб)
Скрипты, которые делают страницу "умнее" =). Их чрезмерное использование может пагубно сказываться на скорости работы сайта.
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=1325115388&amp;format=interactive"></iframe>

### Вес CSS-кода (Кб)
Стили определяют структуру и вид документа. 
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=158869673&amp;format=interactive"></iframe>

### Скорость ответа сервера (мс)
Время, в течение которого браузер ожидает ответа от сервера. Зависит от провайдера, сети, настроек на сервере (кеширование и т.д.), загруженности сервера, а также, что самое важное, скорости работы backend-а. Также есть термин, определяющий этот параметр - "TTFB - Time To First Byte". Другими словами, это то, насколько быстро сервер формирует HTML для вашего пользователя.
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=327297239&amp;format=interactive"></iframe>

### Загрузка DOM (мс)
Следующим шагом является получение HTML от сервера. На этот параметр влияет скорость сети и размер данных.  
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=815551253&amp;format=interactive"></iframe>

### Начало прорисовки (мс)
После того как браузер получит HTML, скачает стили и скрипты, он будет готов к отображению страницы в браузере. Этот параметр называется "firstPaint".
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=672481347&amp;format=interactive"></iframe>

### Завершение загрузки (мс)
Параметр "**pageLoadTime**" фиксирует время полной загрузки страницы, с учётом всех стилей, скриптов и изображений.
<iframe width="569.7781627105671" height="329.024291992188" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1gXQ3wgyhlp77sz0HpVFM03uipu6b4otP6vqGGOk7FvY/pubchart?oid=16441454&amp;format=interactive"></iframe>

##  Подробный разбор проектов
- [Анализ скорости загрузки и работы сайта Bekair.com](http://blog.vesna.kz/analiz-skorosti-zaghruzki-i-raboty-saita-bekair-com/)

Продолжение следует...