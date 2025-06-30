- Используется для управления одним или несколькими контейнерами
- Содержит инструкции по запуску контейнера(ов)
- Упрощает автоматизацию запуска контейнеров
- Описывается в YAML файле: docker-compose.yml
![[Pasted image 20250627154256.png]]

`docker compose up (-d)` - запуск докеркомпос файла

![[Pasted image 20250627154722.png]]

`depends_on: ` - указываем после каких контейнеров запускаться

`docker-compose --version` - это старая версия`
`docker compose version` - это новая версия

`docker compose up -d` - запуск `docker-compose.yml` в фоновом режиме

`docker compose logs -f` - просмотр логов в реальном времени

`docker compose stop` - остановка всех контейнеров `docker-compose.yml`

```
version: '3.5' # версия формата ямл файла
services: # тут указываем наши контейнеры
  ​app: # кон1 с питоном
    image: python # образ
    ports: # порты
      - 80:80
    environment: # переменные
      MYENV=DevOps
    volumes # биндим томы
      - python:/var/python/scripts
  
  db:
  ...
  
volumes: # названия томов они создаются в директории докера
  - python
  - postgresql
```