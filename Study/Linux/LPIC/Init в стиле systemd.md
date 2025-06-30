`Unit` - модули, которыми оперирует `systemd`:
- `.service` - службы
- `.mount` - точки монтирования
- `.device` - устройства
- `.socket` - сокеты
- `.target` - цели

---

`/usr/lib/systemd` - директория с юнитами по умолчанию
`/etc/systemd` - директория с упраляемыми конфигами

---

`systemctl` (system control) - команда для управления демоном `systemd`
`systemctl list-units` - покажет всё запущенные юниты
`systemctl --failed` - покажет юниты которые не запустились 
`systemctl list-units --type=service` - покажет всё запущенные юниты которые отвечают за службы
`systemctl status cron` - покажет статус сервиса `cron`
`systemctl stop cron` - остановка сервиса `cron`
`systemctl start cron` - запуск сервиса `cron`

---

![[Pasted image 20250629115416.png]]

---

`telinit 1` - переключение в однопользовательский режим
`systemctl isolate reboot.target` - запуск цели перезапуск

---

`Journald` - служба журналирования `systemd`
`Systemctl reboot|poweroff|suspend|hibernate|hybrid-sleep`
`Systemctl start|stop|reload|restart|status unit`

---
# Преимущества systemd
- более быстрая загрузка из-за использования паралельных потоков
- более надёжная загрузка, сервисы не подвисают, а если один сервис остановится, остальные не будут ждать
- отслеживает состояние сервисов и может исправлять их
- более надёжная система последовательности
- прекрасная система журналированияы