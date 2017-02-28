# Светофор

Светофор построен на основе [NodeMCU](http://www.nodemcu.com/index_en.html) микроконтроллера с исходным кодом на [micropython](http://docs.micropython.org/en/latest/esp8266/) для ESP-8266.

Светофор имеет 5 независимых ламп:

R1 - красный автомобильный

Y1 - желтый автомобильный

G1 - зеленый автомобильный

R2 - красный пешеходный

G2 - зеленый пешеходный


## Использование

Дли тестирования светофора существует web-инфтерфейс
http://[lighter-ip]/test

Для включения-выключения лампы можно использовать GET-запрос /led/G1/1, /led/G1/0

## Отладка

Для отладки работы модуля светофора возможен мониторинг через серийный порт (через USB)
```# screen /dev/ttyUSB0 115200```

Ctrl+D - софт-перезагрузка модуля
Ctrl+C - переход в консольный режим (выход из http-сервера)

# Связка с JIRA
Связка с JIRA реализовано через скрипт server/task_lighter.py
Скрипт забирает данные с сервиса тестирования (http://webhooks.int.unisender.com:8080/readFileLights)
конвертирует и отправляет POST-запрос для всех цветов на /leds светофора

## Запуск скрипта
```# python task_lighter.py```

## Ошибки
При работе светофора могут возникать ошибки
- горит зеленый пешеходный: светофор потерял wifi.
У модуля существует автоподключение при потере сети,
но иногда он подвисает и нужно передернуть питание
- горит красный пешеходный: ошибка доступа к http://webhooks.int.unisender.com:8080/readFileLights, невозможно получить данные