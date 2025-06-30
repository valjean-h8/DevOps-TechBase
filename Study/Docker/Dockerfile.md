чтобы создать Docker Image
нужно написать Dockerfile

`Dockerfile` - он содержит базовый образ (FROM), описание образа (LABEL), команды (RUN), рабочие директории (WORKDIR), файлы (COPY), работу с файлами, переменные (ENV), порты (EXPOSE), описание команд при запуске контейнера (CMD, ENTRYPOINT)

`docker build .` - создание образа по Dockerfile
`docker tag <image_id> mydocker:v01` - указание тега образа
`docker build -t myimage:v01 .` - создание образа и указание тега

```Dockerfile
FROM ubuntu:22.04
CMD ["echo","Hello my first Dockerfile"]
```

```Dockerfile
FROM ubuntu:22.04
ENTRYPOINT ["echo"] 
# нельзя переопределить, фиксированая команда

CMD ["Hello my second Docker"] 
# можно переопределить в отличие от собрата
```

`CMD` изменяемая команда
`ENTRYPOINT` неизменяемая команда

`LABEL` - через них передаем инфу о докерфайле

`RUN apt update` - говорят если так писать то бывают ошибки хотя у меня не было

`RUN apt-get install nginx -y` - установка с соглашением на скачивание `-y` (yes)

For everyday package management (installing, removing, updating): Use apt. 
For scripting or more advanced package management: Use apt-get. 

лучше юзать в докерфайле apt-get так как меньше вероятность словить неприкольную штуку изза наворотов и современности apt

Если вкратце, то apt разрабатывался для работы в терминале, но не для работы в скриптах и автоматизации. Например, apt отображает индикатор выполнения который будет просто засорять тебе вывод в CI.

во как

# `-it`
- `-i` (от _interactive_) — говорит Docker удерживать стандартный ввод (stdin) открытым. Это нужно, чтобы ты мог вводить команды внутри контейнера.
    
- `-t` (от _tty_) — подключает к контейнеру псевдотерминал, то есть оформляет вывод красиво и удобно, как в обычной командной строке. Без него ты не увидишь привычного форматирования.

`sudo lsof -i :8080` - просмотреть кто занял порт
`curl -Li http://localhost` - вывод страницы по адресу локалхост

`EXPOSE 80` - указываем какие порты юзать в образе 
если по документации ничего нет но помимо этого указываются порты в выводе запущенных контейнеров

`docker run -d --rm --name mydocker -P myimagex:v02`
`-P` - прокидывает рандомные свободные порты к контейнеру

```bash
valjean@ubuntu:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                                                                    NAMES
e0d8d3ee5458   myimagex:v02   "nginx -g 'daemon of…"   4 seconds ago   Up 4 seconds   0.0.0.0:32768->80/tcp, [::]:32768->80/tcp, 0.0.0.0:32769->443/tcp, [::]:32769->443/tcp   mydocker
```

```Dockerfile
COPY files/index.html /var/www/html/
```
аналоги COPY и тега -v
```bash
docker run -d --rm --name mydocker -p 80:80 -v ~/IT/Docker/labs/lab2/files:/var/www/html myimagex:v02
```

`WORKDIR /var/www/html/` - это указываем рабочую директорию, тоесть та директория которя будет у нас изначально как мы зайдём в контейнер так же туда можно сразу копировать файлы

```Dockerfile
WORKDIR /var/www/html/
COPY files/index.html .
```

`ENV OWNER=Valjen` создаём переменную и она будет доступна в контейнере
```bash
docker exec -it mydocker /bin/bash
.....env
...
OWNER=Valjean
```

также переменные можно указывать из командной строки
```bash
docker run -d --rm --name mydocker2 -e TYPE=prod12345 myenv:v01 
```

прикольная штука ищет в файле слова выделенные %USER% и подменяет на ALEX
```
sed -i 's|%USER%|'"ALEX"'|g' ./test-file.txt 
```