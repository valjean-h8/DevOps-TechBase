Работает на транспортном уровне.
Устанавливает соединение.
Работает медленее.
# Как происходит установление соединения:
3-way handshake (трехстороннее рукопожатие):
1. Клиент отправляет серверу запрос с флагом **SYN** (запрос соединения);
2. Сервер отправляет клиенту ответ с флагом **SYN-ACK** (подтверждение);
3. Клиент отправляет серверу запрос с флагом **ACK** (фин подключение).

---

# Как TCP работает с данными:
TCP разбивает поток данных на **сегменты**, нумерует их и ждёт подьверждение от получателя. Если ответа нет - то отправляет повторно.

---

- **TCP** = поток байтов → **сегменты**