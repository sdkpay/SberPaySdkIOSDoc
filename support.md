# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

<br>

# Поддержка

## Обращение в поддержку

> В случае возникновения проблем при интеграции, просьба направлять запрос на: **support@ecom.sberbank.ru**

Для конструктивного разбора проблемы, просьба направлять следующие данные:
1. Видео/ скриншоты процесса оплаты
2. Номер заказа SberPay: `bankinvoiceid`
3. Модель устройства, где происходит оплата
4. Текст/ скрин ошибки
5. Время старта сценария оплаты
6. *Stacktrace* при краше приложения
7. `[LocalSessionID]()` с экрана ошибки/успеха оплаты, из колбэка или с экрана загрузки sdk

<br>

## LocalSessionId

### Идентификатор сессии в SberPay inApp

Идентификатор сессии (`localSessionId`) создается при каждой попытке оплаты через SberPay SDK. Идентификатор используется для разбора инцидентов и отладки работы SDK. `LocalSessionId` можно найти в следующих компонентах:
- На экране загрузки SDK после старта оплаты:

<img src="docs/assets/img/load-pay.png" width="200">

- На результирующих экранах (ошибка/успех оплаты):

<img src="docs/assets/img/success-pay.png" width="200"> <img src="docs/assets/img/fail-pay.png" width="200">

- В коллбеке методов оплаты: <br>Структура [SpaymentResult](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#spaymentresult)
