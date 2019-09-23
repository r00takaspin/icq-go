# 💥 Интеграция go-сервисов в ICQ 💥

##### Вольдэмар Дулецкий, отдел IM, команда ICQ

 ----


# Чем занимаемся? 

## files.icq.com
###### хранение файлов
## go suggest
###### подсказка ответа стикером

---

# go suggest

### подсказка стикером при вводе текста
### предложить ответ стикером на сообщение
### предложить ответ текстом на сообщение

---

![](https://github.com/r00takaspin/icq-go/raw/master/client.png)

--- 

# Стек
## Golang, GitlabCI, RPM, Puppet

---

# ??? IPROS ???

---

# Архитектура

![](https://github.com/r00takaspin/icq-go/raw/master/services.jpg)

---

# Подводные камни

* ipros - бинарный транспортный протокол поверх TCP
* service discovery через внутренний сервис controller
* raw socket read/write
* wire как инструмент DI (удобно для написания тестов)
---

# Боль
* делой pytorch моделей, запакованных в RPM
* структура irpos сообщений жестко не задается на уровне протокола

---
# Итог

Время разработки новых сервисов сократилось за счет современных инструментов Golang.