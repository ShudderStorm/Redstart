Набросок структуры
```
SendMessage:

SUBSCRIBER <- QUEUE               <- CLIENT
^ сервисы     ^ очередь сообщений    ^ вызовы сервисов

ReciveMessage:
SUBSCRIBER -> QUEUE -> CLIENT
           ^push    ^polling
```

Идеи:
 - SUBSCRIBER указаны в конфиге subscribers.json.
 - Сообщения адресуются и принимаются из именованных очередей.
 - QUEUE реплицируется (доп.).
 - Клиенту (пока) доступны все сервисы.
 - KV кэширование сообщений (доп.).

Сценарии CLIENT:

под капотом:
 - discoverSubscribers : map (name, id), err
 - sendMessage : (id, query), err
 - recieveMessage : response, err

пользовательские:
 - SendMessage : (name, query) -> err
 - RecieveMessage : (name) -> chan <-response, err

QUEUE:

Обрабатывает сообщения (Message):

```
type Message struct {
           []rune payload
           int id
           int sender
           int reciever
}
```
