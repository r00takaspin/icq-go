# 💥 Интеграция go-сервисов в ICQ 💥

##### Вольдэмар Дулецкий, отделение IM, команда ICQ

 ----


# Чем занимаемся? 

## files.icq.com
###### хранение файлов
## go suggest
###### подсказка ответа стикером

---

# go suggest

### предложить заменить вводимый текст стикером
### ответ стикером на сообщение
### ответ текстом на сообщение

---

![](https://github.com/r00takaspin/icq-go/raw/master/client.png)

--- 

# Стек
## Golang, GitlabCI, RPM, Puppet

---

# Ipros?

---

# Архитектура

![](https://github.com/r00takaspin/icq-go/raw/master/services.jpg)

---

# Технологии

* ipros - бинарный транспортный протокол поверх TCP
* service discovery через внутренний сервис controller
* raw socket read/write
* wire как инструмент DI (удобно для написания тестов)
---

# Боль
* делой pytorch моделей, запакованных в RPM
* структура ipros сообщений жестко не задается на уровне протокола

---
# Итог

Увеличение скорости разработки сервисов относительно времени, затрачиваемому на разработку аналогичных сервисов на C/C++.