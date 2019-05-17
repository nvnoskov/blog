+++
date = "2015-08-03T19:52:59+06:00"
draft = false
title = "Meteor Shop: Скорость загрузки и работы сайта- почему она важна. Часть 1"
slug = "meteor-shop-skorost-pochiemu-ona-vazhna"
image = "/2015/08/speed-up-website-load-times-featured.png"
aliases = [
	"meteor-shop-skorost-pochiemu-ona-vazhna"
]
author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++
[Andy Hume](https://twitter.com/andyhume) - Разработчик в Twitter, в прошлом разработчик в Microsoft, Guardian
> There is no difference for the user between a site **down** and site beign **inaccessable** due to loading issues caused by blocking resources or slow networks.

Очень интересная мысль заключается в том, что для пользователя нет никакой разницы между неработающим и медленным сайтом.

Вопрос скорости загрузки сайта стал более актуален с ростом популярности мобильных устройств.
По данным kurs.kz, в июле 2015 года, 51% посетителей использовали мобильные устройства. Для сравнения в августе 2014 году их доля составляла 32%, а в 2013 году - 18%. 

<div id="chart_div"></div>

## Ощущение скорости и UX (User Experience)
![](/images/2015/08/ux_5_components_cover-1080x675.jpg)
Изображение взято с [How To Improve Your Website User Experience](http://kleurvision.com/improve-your-website-user-experience/)
> **UX** - Международный стандарт ISO 9241-210[1] определяет опыт взаимодействия как «ощущение и реакцию человека, вследствие использования или предполагаемого использования продукта, системы или услуги»

*Простым языком, **UX** это то, насколько ваша веб-страница выполняет поставленную перед ней задачу. Например, доносит контактную информацию, агитирует на покупку и т.д.*

Крайне важно чтобы ваши пользователи получали информацию как можно быстрее.   Потому что борьба за внимание вашего посетителя, начинается **с первой секунды**.

> Никто не любит ждать.

Для концентрированного внимания пользователя, считается самым оптимальным получение информации с задержкой **не более 1 секунды**. Если же информация подгружается дольше, это становиться заметным для него. А если задержка получения информации длится более 2.5 секунд, то внимание пользователя рассеивается.

[WebPageTest](http://www.webpagetest.org/) специально определили так называемый "**Speed Index**" в котором измеряется скорость открытия страницы.
А также вывели его оптимальное значение в **1000**.

Примечание: Для того чтобы значение было 1000 или ниже, нужно чтобы "==Critical Render Path=="  умещался в первые 14 КБайт вашей страницы, что практически нереально.

Давайте посмотрим примеры загрузки сайтов чтобы представлять о чём идёт речь (Примеры были проведены на скорости 1Мбит/с).

[Тест Sports.kz](http://www.webpagetest.org/result/150803_9Q_PKR/) - Speed Index = 10813 (0.869s - первый байт, 8.788s - начало отображение, 35.721s	 - полная загрузка)
<iframe src="http://www.webpagetest.org/video/view.php?id=150803_9Q_PKR.1.0&embed=1&width=520&height=432" width="520" height="432"></iframe>

[Тест Tengrinews.kz](http://www.webpagetest.org/result/150803_SS_PCH/) Speed Index = 11810 (0.438s	 - первый байт, 6.312s - начало отображение, 16.420s	 - полная загрузка)
<iframe src="http://www.webpagetest.org/video/view.php?id=150803_SS_PCH.1.0&embed=1&width=520&height=432" width="520" height="432"></iframe>

[Тест SmashingMagazine.com](http://www.webpagetest.org/result/150803_10_Q0Z/) Speed Index = 4197 (	0.949s		 - первый байт, 1.681s - начало отображение, 7.508s	 - полная загрузка)
<iframe src="http://www.webpagetest.org/video/view.php?id=150803_10_Q0Z.1.0&embed=1&width=520&height=432" width="520" height="432"></iframe>

[Тест Theguardian.com](http://www.webpagetest.org/result/150803_K8_Q2E/) Speed Index = 3707	 (0.671s - первый байт, 	3.516s - начало отображение, 4.187s	 - полная загрузка)
<iframe src="http://www.webpagetest.org/video/view.php?id=150803_K8_Q2E.1.0&embed=1&width=520&height=432" width="520" height="432"></iframe>


В следующих статьях я более подробнее опишу подробнее инструменты для измерения производительности и отдельной статьёй опишу что такое **"60 fps Site"**

<script type="text/javascript" src="https://www.google.com/jsapi"></script>

<script type="text/javascript">
google.load('visualization', '1', {packages: ['corechart', 'line']});
google.setOnLoadCallback(drawBasic);

function drawBasic() {

      var data = new google.visualization.DataTable();
      data.addColumn('number', 'X');
      data.addColumn('number', 'Desktop');
      data.addColumn('number', 'Mobile');


      data.addRows([
        [2013, 76.93, 23.07],   
        [2014, 62.70, 37.30],   
        [2015, 48.79, 51.21],   
      ]);

      var options = {
        hAxis: {
          title: 'Год'
        },
        vAxis: {
          title: '% Пользователей'
        }
      };

      var chart = new google.visualization.LineChart(document.getElementById('chart_div'));

      chart.draw(data, options);
    }
</script>