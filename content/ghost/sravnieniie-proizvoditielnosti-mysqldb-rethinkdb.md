+++
date = "2016-01-14T13:28:26+06:00"
draft = false
title = "Сравнение производительности PHP5.6, PHP7, NodeJS, Go"
slug = "sravnieniie-proizvoditielnosti-mysqldb-rethinkdb"
aliases = [
	"sravnieniie-proizvoditielnosti-mysqldb-rethinkdb"
]
tags = ["Go", "PHP7", "Производительность","Mysql","RethinkDB"]
author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++
## Оптимизация
Задумавшись над оптимизацией производительности одного из проектов, захотелось привести ряд замеров скорости на разных базах и платформах.

Чтобы не затрагивать аспекты производительности фреймворков (роутинг, работа с шаблонами) я старался минимально протестировать скорость инициации соединения с базой и запрос на получение данных.

И вот что из этого вышло:

<iframe width="700" height="400" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/16j_2VuqbnnF04v929XTceJ9vHRksOSFOVBx7B7rjVJ8/pubchart?oid=1205557003&amp;format=interactive"></iframe>