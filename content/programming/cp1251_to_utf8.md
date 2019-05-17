+++
date = "2016-02-09T18:47:02+06:00"
draft = false
title = "Перевод проекта из кодировки CP1251 в UTF-8"
image = "code.jpg"

author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++

## Кодовая база проекта

Можно воспользоваться таким вариантом в виде "почти одной" команды.
```bash
for FILE in $(find /project -name '*.php'); 
	do mv $FILE{,.orig} && iconv -f CP1251 -t UTF-8 $FILE.orig -o $FILE; 
done
```

Или можно использовать простой BASH-скрипт
```bash
#!/bin/bash

# Рекурсивная конвертация windows-1251 --> utf-8
# Напримере файлов *.php, *.html, *.css, *.js.

find ./project -name "*.php" -o -name "*.html" -o -name "*.css" -o -name "*.js"  -type f |
while read file
do
  echo " $file"
  mv $file $file.icv
  iconv -f WINDOWS-1251 -t UTF-8 $file.icv > $file
  rm -f $file.icv
done
```

## База данных (Mysql)

Тут особенностей гораздо больше. Приведу пример который подошёл для меня.

```bash
mysqldump -u user -p password database_cp1251 > dump_cp1251.sql
sed 's/cp1251/utf8/g' dump_cp1251.sql > dump_utf8.sql
mysql -u user -p password database_utf8 < dump_utf8.sql
```
Есть вариант возникновения ошибки **#1071 - Specified key was too long; max key length is 1000 bytes**. 
Фиксится удалением текстовых ключей проблемной таблицы.


