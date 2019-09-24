# 💥 Интеграция go-сервисов в ICQ 💥

![x% center](https://github.com/r00takaspin/icq-go/raw/master/mascot.jpg)
===

##### Вольдэмар Дулецкий, команда ICQ
![v.duletskiy@corp.mail.ru]v.duletskiy@corp.mail.ru

 
 ----

# Чем занимаемся? 

## files.icq.com
###### хранение файлов
## go suggest
###### подсказка ответа стикером

---

![](https://github.com/r00takaspin/icq-go/raw/master/suggest.png)

---


# go suggest

### предложить заменить вводимый текст стикером
### ответ стикером на сообщение
### ответ текстом на сообщение

--- 

# Стек
## Golang, Gitlab, RPM, Puppet

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