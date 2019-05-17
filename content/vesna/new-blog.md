+++
date = "2016-02-02T21:01:35+06:00"
draft = false
title = "Новый блог на HUGO"
image = "hugo.png"
author = "Nikolay Noskov"
email = "nvnoskov@gmail.com"
+++


### Go и путь Gopher-а

Совсем не так давно я изучая просторы Go, я наткнулся на проект [Hugo](https://gohugo.io).
Проект представляет собой генерацию статичных страниц на основе файлов формата markdown.

Так как у меня в голове давно засела мысль о "скоростном вебе", я незамедлительно решил что перенесу блог весны на платформу [Hugo](https://gohugo.io).

Основных причин было две:

 - Сделать блог быстрым, ghost не радовал скоростью
 - Изучить подробнее Go и его работу с вебом.

### Сказано-сделано

Первым делом надо перенести старые записи в новый формат. Есть чудесный скрипт [GhostToHugo](https://github.com/jbarone/ghostToHugo). 
Обрабатываем им выгруженные даннее из Ghost и всё можно запускать Hugo.

```
hugo server -w 
```

По умолчанию он запускает сервер по адресу localhost:1313, при желании его можно сменить.

### Выгрузка на сервер. Docker.

Небольшой поиск готовых решений на [Docker Hub](https://hub.docker.com) и я остановился на образе [**jojomi/hugo**](https://github.com/jojomi/docker-hugo).

Файл run.sh который является *точкой входа* docker-контейнера. Основными параметрами при запуске сервера на которые стоит обратить внимание являются 
*---source="/src" и --destination="/output"*
т.е. путь к проекту на Hugo и место куда сложить статику.

#### Файл run.sh
```bash
#!/usr/bin/env sh

WATCH="${HUGO_WATCH:=false}"
SLEEP="${HUGO_REFRESH_TIME:=-1}"
echo "HUGO_WATCH:" $WATCH
echo "HUGO_REFRESH_TIME:" $HUGO_REFRESH_TIME
echo "HUGO_THEME:" $HUGO_THEME
echo "HUGO_BASEURL" $HUGO_BASEURL

HUGO=/usr/bin/hugo

while [ true ]
do
    if [[ $HUGO_WATCH != 'false' ]]; then
	    echo "Watching..."
        $HUGO server --watch=true --source="/src" --theme="$HUGO_THEME" --destination="/output" --baseUrl="$HUGO_BASEURL" || exit 1
    else
	    echo "Building one time..."
        $HUGO --source="/src" --theme="$HUGO_THEME" --destination="/output" --baseUrl="$HUGO_BASEURL" || exit 1
    fi

    if [[ $HUGO_REFRESH_TIME == -1 ]]; then
        exit 0
    fi
    echo "Sleeping for $HUGO_REFRESH_TIME seconds..."
    sleep $SLEEP
done
```

> Немного о том как работает Hugo. На основе .md файлов и шаблона темы он генерирует готовые html которые являются **полностью статичными**.

Т.е. на выходе мы получим лишь статичные файлы которые мы покажем пользователям. А кто справится с этой задачей лучше чем nginx?

Связываем 2 контейнера между собой при помощи [docker-compose](https://docs.docker.com/compose/).

#### Файл docker-compose.yml
```yaml
hugo:
  image: jojomi/hugo:latest
  volumes:
    - ./blog.vesna.kz/:/src
    - ./output/:/output
  environment:
    - HUGO_REFRESH_TIME=3600
    - HUGO_THEME=robust
    - HUGO_WATCH=false
    - HUGO_BASEURL=http://blog.vesna.kz
  restart: always

web:
  image: jojomi/nginx-static
  volumes:
    - ./output:/var/www
  environment:
    - VIRTUAL_HOST=blog.vesna.kz
  ports:
    - "80:80"
  restart: always
```

Запускаем

```bash
docker-composer -f docker-compose.yml up
```

### Итог 

На хостовой машине мы получаем nginx на 80-м порту, который показывает содержимое статичной папки блога. Которая в свою очередь генерится каждый час на основе файлов из проекта Hugo.

```
root@blog:~# docker ps
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS                         NAMES
1a0419db8e6b        jojomi/hugo:latest    "/run.sh"           17 hours ago        Up 17 hours         1313/tcp                      root_hugo_1
6dab6f20a315        jojomi/nginx-static   "nginx"             17 hours ago        Up 17 hours         0.0.0.0:80->80/tcp, 443/tcp   root_web_1

```

Нам остаётся лишь писать новые записи в блог и пушить их на сервер

```bash
hugo new vesna/blog.md
git add vesna/blog.md
git commit -m "Новая запись в блоге"
git push production master
```

That`s all folks! 

