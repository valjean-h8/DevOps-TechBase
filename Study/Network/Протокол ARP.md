**`ARP (Address Resolution Protocol)`** - протокол, суть которого в том, чтобы узнать какой `MAC-адрес` соответствует заданному `IP-адресу`, чтобы можно было отправить данные по физ сети.

Как работает ARP (пошагово):
1. Устройство знает IP, но не MAC — запускает ARP-запрос.
2. Все устройства в сети получают его, но **только владелец IP** отвечает.
3. MAC-адрес сохраняется в **ARP-таблице**, чтобы не спрашивать повторно.
4. Данные передаются по MAC в Ethernet-кадре.