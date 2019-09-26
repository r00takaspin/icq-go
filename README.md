![bg left:30% 70%](https://github.com/r00takaspin/icq-go/raw/master/mascot.jpg)

# <!--fit-->Интеграция go-сервисов в ICQ

###### Вольдэмар Дулецкий, команда ICQ

[v.duletskiy@corp.mail.ru](v.duletskiy@corp.mail.ru)
 
 ---

# <!--fit-->Введение
- много продуктовых задач
- много уже существующих сервисов со сложившейся инфраструктурой
- задачи требуют быстрого внедрения
- на C/C++ долго

---

# <!--fit-->Чем занимаемся? 

---

# <!--fit--> files.icq.com
# __хранение файлов__
## PHP, Golang, MySQL, Tarantool

---

# <!--fit-->go suggest
# __подсказка ответа стикером__
# Golang, ML, ipros 
---

![bg 50%](https://github.com/r00takaspin/icq-go/raw/master/suggest.png)

---

## На основе ML 

1. предложить заменить вводимый текст стикером
1. ответ стикером на сообщение
1. ответ текстом на сообщение

--- 

## Golang, Gitlab, RPM, Puppet
###### дефолтный стек mail.ru
---

# <!--fit-->ipros?
###### 12 байт должно хватить каждому

---

# <!--fit-->Структура пакета

---

![bg fit 70%](https://github.com/r00takaspin/icq-go/raw/master/iproto.png?123)

---


# <!--fit-->Содержимое пакета

---
![bg fit 69%](https://github.com/r00takaspin/icq-go/raw/master/ds.png?1234)

---

# TLV


###### очень полезная структура  

---

Пример кода

```golang
func HandshakePayload(svc string, host string, cfg string) []byte {
  return TLVPack(
       SLPack([]byte(svc)),
       SLPack([]byte(host)),
       SLPack([]byte(cfg)),
  )
}

```

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/services.jpg)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/1.png)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/2.png)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/3.png)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/4.png)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/5.png)

---

![bg center 70%](https://github.com/r00takaspin/icq-go/raw/master/arch/6.png)

---
# JSON запрос
```
POST /suggest HTTP/1.1
Host: 127.0.0.1:8080
User-Agent: Go-http-client/1.1
Content-Length: 178
Content-Type: application/json
Accept-Encoding: gzip

{"msgs":
   [
      {"sender":"7105550","receiver":"7105551","TS":1564997991,"text":"тест"},
      {"sender":"7105551","receiver":"7105550","TS":1564997991,"text":"тест"}
   ]
}
```

178 байт

---

# gRPC  запрос
```protobuf
message Request {
  repeated Msg message = 1;
}

message Msg {
  string sender     = 1;
  string receiver   = 2;
  uint32 TS         = 3;
  string text       = 4;
}

```
162 байта

---

# Ipros запрос
```binary
 01 00 00 00 7b 00 00 00  42 04 cb 9a 01 00 00 00  |....{...B.......|
 07 00 00 00 37 37 30 31  35 31 34 01 00 00 00 64  |....7701514....d|
 00 00 00 02 00 00 00 5c  00 00 00 03 00 00 00 26  |.......\.......&|
 00 00 00 07 00 00 00 37  31 30 35 35 35 30 07 00  |.......7105550..|
 00 00 37 31 30 35 35 35  31 3d 24 8a 5d 08 00 00  |..7105551=$.]...|
 00 d1 82 d0 b5 d1 81 d1  82 03 00 00 00 26 00 00  |.............&..|
 00 07 00 00 00 37 31 30  35 35 35 31 07 00 00 00  |.....7105551....|
 37 31 30 35 35 35 30 3d  24 8a 5d 08 00 00 00 d1  |7105550=$.].....|
 82 d0 b5 d1 81 d1 82                              |.......|
```
123 байта

---

# ipros соединение

1. соединение с контроллером (service discovery)
1. получение списка хостов, шардированных по ключу
1. выбор хоста
1. handhake
1. обмен данными

---

# Почему не gRPC?
 1. во многих  крупных компаниях есть свой RPC
 1. ipros экономит трафик
 1. исторически так сложилось

---

# Боль
1. деплой ML моделей, запакованных в RPM
1. структура ipros сообщений жестко не задается на уровне протокола

---
# Как избавились от боли?

1. ручная сборка nmslib
1. написана библиотека для работы с бинарными данными
1. ipros: с нуля написан клиент и сервер

---

# // TODO

```golang
type Message struct {
    string Sender     `iproto:"sl"`
    string Receiver   `iproto:"sl"`
    uint32 TS         `iproto:"."`
    string Text       `iproto:"sl"`
}


type Request struct { 
   uint32 MsgType     `iproto:"."`
   string Sender      `iproto:"sl"`
   []Message Messages `iproto:"sl"`
}
...

r := &Request{}
ipros.Unmarshal(data, r)
```
######  *сделать работу с бинарными данными еще проще
---
# Итог

Увеличение скорости разработки сервисов относительно времени, затрачиваемому на разработку аналогичных сервисов на C/C++.

---

![bg right:50% 70%](https://github.com/r00takaspin/icq-go/raw/master/qr.png)
# <!--fit-->Спасибо!

###### [https://github.com/r00takaspin/icq-go](https://github.com/r00takaspin/icq-go)