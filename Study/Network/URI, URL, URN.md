# Что такое URI?
`URI (Uniform Resource Identifier)` - это унифицированный идентификатор ресурса

---

Примеры `URI`:
- `https://example.com/index.html`
- `mailto:info@example.com`
- `ftp://ftp.example.com/file.txt`

---

```
scheme://user:password@host:port/path?query#fragment
```

Разберём по частям:

- **scheme** — схема доступа: `http`, `https`, `ftp`, `mailto`, `file`, и т.д.
- **host** — адрес сервера: `example.com`, `localhost`, `192.168.0.1` и др.
- **port** _(необязательно)_ — номер порта, например `:443` для HTTPS.
- **path** — путь до файла/ресурса: `/images/pic.jpg`
- **query** _(необязательно)_ — параметры запроса: `id=42&sort=desc`
- **fragment** _(необязательно)_ — якорь на странице: `#section3`

---

> URI = URL + URN

---

# Что такое URL?
`URL (Uniform Resource Locator)` - это подмножество `URI`, которое **уточняет местоположение ресурса и способ доступа**.

> URL — это то, что ты вводишь в браузере, чтобы получить страницу, файл или API-ответ.

---

# Что такое URN?
`URN (Uniform Resource Name)` - это уникальное имя ресурса в заданной области, **без указания его местонахождения или способа доступа**.