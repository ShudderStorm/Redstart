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

Сценарии CLIENT:
под капотом:
 - discoverSubscribers : map (name, id), err
 - sendMessage : (id, query), err
 - recieveMessage : response, err
пользовательские:
 - SendMessage : (name, query) -> err
 - RecieveMessage : (name) -> chan <-response, err


