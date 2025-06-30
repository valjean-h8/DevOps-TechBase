при запуске докера получаем сетевой интерфейс `docker0`
```
 docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 4a:68:40:a6:9c:ab brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
```

по умолчанию докер предоставляет несколько типов сетей:
- `bridge` - тип сети по умолчанию (172.17.0.0/16)
  контейнеры сразу получают доступ в наружу
  так же можем подключится из вне для этого нужно создать мости при помощи `-p 80:80` (например)
- `host` - если хотим запустить контейнер в сети хоста 
  `docker run nginx --network=host` можем подключиться локально через `ip addres`
- `none` - 'docker run nginx --network=none' мы не сможем зайти локально или через айпи
это три типа сетей которые создаются автоматически
- `macvlan`
- `ipvlan`
- `overlay (Docker Swarm Cluster)`

### `BRIDGE`
`docker network create --drive brifge <NAME>` - создание сети типа `bridge`
`docker run --net myNAME nginx` - запуск контейнера в определенной сети
контейнеры могут уже общаться между собой в этой сети
они могут общаться по ДНС именам или адресам
сети не могут общаться между собой
![[Pasted image 20250626105409.png]]

### `HOST`
`--drive host` 
сервер может подключаться к ним
и используют контейнеры адресс хоста
![[Pasted image 20250626105528.png]]

### `NONE`
`--drive none`
самый простой тип который редко используется
контейнеры изолированны друг от друга
![[Pasted image 20250626105639.png]]

В основном используется `bridge`, `host`.

### `macvlan`
контейнеры получают свои мак-адреса
и им присваюваются свои сетевые карты и айпи адреса
и можно подключится через адреса а не порты
![[Pasted image 20250626110002.png]]

### `ipvlan`
похоже не `macvlan`но мак адрес не изменяется
![[Pasted image 20250626110100.png]]

`docker network ls`
`docker network create myNet01`

мы не можем создать больше одного типа `host` `null`

`docker network inspect <name_network>`
`docker network create -d bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 myNet192`
`docker network rm <name_network>`

`docker network connect myNet01 container1`
`docker network disconnect <NetworkID> container1`
`docker run --rm -it --name container1 --ip 10.10.10.213 --net myHomeLan nicolaka/netshoot /bin/bash`
