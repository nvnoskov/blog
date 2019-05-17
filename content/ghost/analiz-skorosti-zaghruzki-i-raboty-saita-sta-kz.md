+++
date = "2015-08-27T10:29:52+06:00"
draft = false
title = "Анализ скорости загрузки и работы сайта Scat.kz"
slug = "analiz-skorosti-zaghruzki-i-raboty-saita-sta-kz"
aliases = [
	"analiz-skorosti-zaghruzki-i-raboty-saita-sta-kz"
]
tags = ["Метеор", "Скорость"]
categories = ["PageSpeed"]
author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++

Следующий на очереди Scat.kz, с показателем firstPaint в 730мс.

## Основные показатели
![](/images/2015/08/screen_023.png)

## Загрузка документа
Общий объём документа в 2.6мб. Сайт полностью грузится за 14.52 секунды. 
Основной объём страницы в картинках, так же сильно смущает TTFB в 555мс, при отдаче статики. Это говорит либо о неправильных настройках сервера, либо его нагрузке при отдаче статики.
![](/images/2015/08/screen_025.png)

## PageSpeed ==57 / 100==
[Отчёт PageSpeed](https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fwww.scat.kz%2Fru%2F&tab=desktop)

Основные рекомендации:

* Сжатие картинок. Загруженные картинки не оптимизированы под веб. (Сохранение JPG с качеством не более 75 и удаление EXIF информации) 
* На сервере отключено сжатие и кеширование статики необходимо его обязательно настроить. 