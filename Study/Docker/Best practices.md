1. **ИСПОЛЬЗОВАТЬ `EXEC FORM`**:
	- `shell form - ENTRYPOINT node app.js`
	- `shell form - ENTRYPOINT ["node","app.js"]`
	 В чём разница и почему лучше использовать `exec form`?
	 
- ENTRYPOINT ["node", "app.js"]
```bash
$ docker exec 4675d ps x  
PID TTY      STAT   TIME    COMMAND
1    ?        Ssl    0:00   node app.js   
12   ?        Rs     0:00   ps x
```

---

- ENTRYPOINT node app.js
```bash
$ docker exec -it e4bad ps x  
PID TTY      STAT   TIME    COMMAND    
1    ?        Ss     0:00   /bin/sh -c node app.js
7    ?        Sl     0:00   node app.js   
13   ?        Rs+    0:00   ps x
```

если ты запускаешь `node app.js` через shell form — процесс `node` не будет PID 1, и Docker не сможет правильно следить за ним.

2. **УКАЗЫВАТЬ В ОБРАЗАХ КОНКРЕТНЫЕ ВЕРСИИ**
		`from python:3.12.3`

