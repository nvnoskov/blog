+++
date = "2016-03-24T14:35:08+06:00"
draft = false
title = "Сравнение производительности RethinkDB на NodeJS и Go"
image = "rethink-node-go.png"
tags = ["Go", "NodeJS", "Производительность", "RethinkDB"]

author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++

## Выбор платформы для работы RethinkDB

Твёрдо решив что всё таки стоит попробовать использовать RethinkDB в качестве базы данных, я задался какой же платформой воспользоваться для  создания REST API.

Раннее я [сравнивал](/ghost/sravnieniie-proizvoditielnosti-mysqldb-rethinkdb/) RethinkDB c Mysql на различных платформах.
Тест был тривиален и содержал лишь в себе инициацию соединения с БД и один запрос на выборку данных.

<iframe width="700" height="400" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/16j_2VuqbnnF04v929XTceJ9vHRksOSFOVBx7B7rjVJ8/pubchart?oid=1205557003&amp;format=interactive"></iframe>


## NodeJS или Go

На графике понятно только одно, что "только не PHP". Хотя PHP7 весьма неплох.

Теперь пора провести более серьёзный тест на вставку, выборку и удаление данных. За основу я возьму архив изменений валютного курса с [kurs.kz](http://kurs.kz)

В файле имеются 4114 значений такого вида.
```json
[{
    "id": "2",
    "newdate": "1095206400",
    "usd_buy": "135.4500",
    "usd_sell": "135.9500",
    "eur_buy": "165.2500",
    "eur_sell": "166.8500",
    "rur_buy": "4.6000",
    "rur_sell": "4.6500"
},
... ]
```
## NodeJS
### NodeJS множественная вставка (bulk insert)

```bash
time curl localhost:3000/insert

real    0m0.811s
user    0m0.004s
sys 0m0.004s
```


### NodeJS выборка
#### Без обработки результатов

Т.е первый отклик системы после запроса

```js
r.table('archive').run(conn, function(err, res){
  if(err) throw err;
  response.end();
});
```
```bash
time curl localhost:3000/select

real    0m0.077s
user    0m0.008s
sys 0m0.000s
```

#### С обработкой результатов (toArray)

```js
r.table('archive').run(conn, function(err, res){
    if(err) throw err;
    res.toArray(function(err, data){
        console.log(err,data.length)
        response.end();
    });
});
```

```bash
time curl localhost:3000/select

real    0m0.201s
user    0m0.004s
sys 0m0.004s
```

### NodeJS массовое удаление

```js
r.table('archive').delete()
```

```bash
time curl localhost:3000/delete

real    0m0.236s
user    0m0.004s
sys 0m0.004s

```

### NodeJS построчное удаление
Здесь уже простым замером времени выполнения запроса не выйдет, так как тут множество асинхронных запросов (4114 шт.).
Потому такой "костыль".
(И да я не учитываю время фактического выполнения команды на удаление, лишь сколько занимает "прокрутка" всех данных и запрос на их удаление.)
```js
res.each(function(err, row){
    r.table('archive').get(row.id).delete().run(conn);
}, function(){
    console.log(+new Date()-start); // Завершение  выборки
});
```
```bash
==>  780 ms
```

## Go

### Go множественная вставка (bulk insert)

```go
r.DB("test").Table("archive").Insert(archives).Run(session)
```
```bash
[GIN] 2016/03/25 - 11:45:29 | 200 |  482.971048ms | 127.0.0.1 |   GET     /index
```


### Go выборка с приведением к интерфейсам (массиву)

```go
rows, err := r.DB("test").Table("archive").Run(session)
if err != nil { fmt.Println(err)}
var selectedArchives []Archive
errParse := rows.All(&selectedArchives)
if errParse != nil { fmt.Printf("Error scanning database result: %s", errParse) }
fmt.Printf("%d selectedArchives", len(selectedArchives))
```
```bash
[GIN] 2016/03/25 - 11:51:12 | 200 |  210.791357ms | 127.0.0.1 |   GET     /select
```



### Go массовое удаление

```go
r.DB("test").Table("archive").Delete().Run(session)
```
```bash
[GIN] 2016/03/25 - 11:47:22 | 200 |  157.572104ms | 127.0.0.1 |   GET     /delete
```

## Результаты
Они весьма равные. Мне казалось что Go победит с большим отрывом.
<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/1_RvFqRXL4pn2f6czZmjbU_B8gI3hG4HqWhApM79y6Zg/pubchart?oid=1150232941&amp;format=interactive"></iframe>

## P.S
Тесты проводились на машине AMD FX-8320E x 8, 16Gb


