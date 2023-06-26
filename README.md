# Vakio Atmosphere

Интеграция для Homeassiant, позволяющая управлять устройством Vakio Atmosphere.

Для корректной работы интеграции требуется выполнить следующие шаги:
1. [Установка MQTT-брокера](#broker)
    1. [Установка дополнения](#broker_download)
    2. [Настройка брокера](#broker_settings)
2. [Подключение прибора к брокеру](#connect)
3. [Установка интеграции](#setup)

Если столкнулись с ошибками:
- [Возможные ошибки и способы их решения](#errors)
---

## <a name="broker"></a> 1. Установка и настройка MQTT-брокера

Данный этап можно пропустить, если у вас уже есть брокер.

Установка брокера производится в рамках Homeassitant.

### <a name="broker_download"></a> 1. Установка дополнения

1. В Homeassistant перейдите в **Настройки** -> **Дополнения** -> **Магазин дополнений**.
2. Найдите "Mosquitto broker" и нажмите на него.
3. Нажмите кнопку "Установить".
4. После окончания установки нажмите "Запустить".
5. Переведите слайдер "Автозагрузка" в положение **ВКЛ**.

### <a name="broker_settings"></a> 2. Настройка брокера

Данный этап является необязательным.

1. В Homeassistant перейдите в **Настройки** -> **Дополнения**.
2. Найдите "Mosquitto broker" и нажмите на него.
3. Нажмите кнопку "Запустить", если не сделали это ранее.
4. <a name="broker_normal_mqtt"></a> Во вкладке "Конфигурация" можно изменить порт "Normal MQTT", если требуется.

---

## <a name="connect"></a> 2. Подключение прибора к брокеру

Ознакомьтесь с <a target="_blanc" href="https://vakio.ru/vakio-mqtt.pdf">Инструкцией по подключению приборов по MQTT</a>.

Заполните поля в разделе "Настройка MQTT" следующим образом:
1. **Имя сервера MQTT** - ip-адрес сервера Homeassistant.
2. **Порт** - порт "Normal MQTT" ([пункт 1.2.4](#broker_normal_mqtt)), по умолчанию 1883.
3. **Логин** - не заполняется.
4. **Пароль** - не заполняется.
5. **Топик** - произвольно*.

\* *каждый прибор должен иметь уникальный топик.*

***Пример***
```
Имя сервера MQTT: 192.168.0.10
Порт: 1883
Логин:
Пароль:
Топик: vakio_atmo1
```

## <a name="setup"></a> 3. Установка интеграции

1. В Homeassistant перейдите в **Настройки** -> **Устройства и службы** -> **Добавить  интеграцию**.
2. Найдите бренд "Vakio" и нажмите на него.
3. Выберите интеграцию, опираясь на наименование.
4. В появившемся окне введите значения, которые вводили в пункте [2. Подключение прибора к брокеру](#connect)

---

## <a name="errors"></a> Возможные ошибки

### <a name="auth_error"></a> **Не удалось авторизироваться**

- Проверьте корректность введенных данных брокера (Хост, порт, имя пользователя и пароль).
- Если всё заполнено правильно, проверьте, запущено ли дополнение:
    1. В Homeassistant перейдите в **Настройки** -> **Дополнения**.
    2. Найдите "Mosquitto broker" и нажмите на него.
    3. В нижней части должны быть доступны кнопки "Остановить" и "Перезапустить".

### <a name="auth_error"></a> **Значение сенсора "Неизвестно"**

- Перезагрузите прибор путём полного отключения из сети. Дождитесь полного включения устройства, если в течение минуты значения не появились, переходите к следующему пункту.
- Измените топик в устройстве на другой, переустановите интеграцию на новый топик.