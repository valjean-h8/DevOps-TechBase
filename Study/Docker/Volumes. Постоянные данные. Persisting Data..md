если мы вносим какие-то изменения в контейнере и убиваем его то данные не сохраняются

как их сохранить???
мы можем хранить их на хосте и смонтировать их к контейнеру
это называется Persisting Data (Сохраняющиеся данные)

Есть три способа как это сделать:
1. HOST VOLUMES
	`docker run -v /opt/mysql_data:/var/lib/mysql mysql`
	`docker run -v /opt/app_conf:/etc/app/configs app`
	 слева часть хоста : справа часть контейнера
	 ![[Pasted image 20250625231617.png]] 
2. ANONYMOUS VOLUMES
	 `docker run -v /var/lib/mysql mysql`
	 `docker run -v /etc/app/congigs app`
	 монтируется в путь var/lib/docker/volumes/HASH/_data и там хранятся данные и HASH сам генерируется
	 ![[Pasted image 20250625231947.png]]
      
3. NAMED VOLUMES
	`docker run -v mysql_data:/var/lib/mysql mysql`
	`docker run -v app_conf:/etc/app/configs app`
	 сохраняется по пути var/lib/docker/volumes/mysql_data/_data
	 так же и со второй командой только наименование другое
	 ![[Pasted image 20250625232300.png]]

`docker volume ls` - просмотр имеющихся volumes
`docker volume create <name_volume>` - создание volume
`docker volume rm <name_volume>` - удаление тома (volume)