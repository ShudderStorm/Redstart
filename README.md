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
 - QUEUE реплицируется (доп.).
 - Клиенту (пока) доступны все сервисы.
 - KV кэширование сообщений (доп.)

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

Для каждого подписчика $S_i$ определена очередь $Q_i$, сообщения, адресованные $S_i$ от клиента $C_j$ складываются $Q_{ij}$
