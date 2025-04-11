# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

# Вспомогательные структуры данных

## Параметры для инициализации SberPay SDK

#### Параметры для передачи в функцию `setup`

|Параметр|Тип|Дефолтное значение|Обязательный|Описание|
|---|:---:|:---:|:---:|---|
|bnplPlan|Bool|true|Нет|Функционал «Оплата частями»|
|spasiboBonuses|Bool|true|Нет|Функционал бонусов «Спасибо»|
|resultViewNeeded|Bool|true|Нет|Отображение экранов со статусом|
|helpers|Bool|true|Нет|Функционал Helpers (Помогашки)|
|needLogs|Bool|true|Нет|Выведение логов в консоль в режиме песочницы|
|helperConfig|SBHelperConfig|-|Да|Настройки функционала Helpers (Помогашки).<br>Структура [SBHelperConfig](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#sbhelperconfig)|
|environment|SEnvironment|prod|Нет|Выбор окружения sdk для работы.<br>Структура [SEnvironment](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#senvironment)|
|completion|((SPError?) -> Void)?|-|Да|Блок, отрабатыващий после инициализации SDK.<br>Структура [SPError](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#sperror)|

<br>

## SBHelperConfig

|Параметр|Тип|Дефолтное значение|Обязательный|Описание|
|---|:---:|:---:|:---:|---|
|sbp|Bool|true|Нет|Разрешить пополнение карты через СБП|
|creditCard|Bool|true|Нет|Разрешить выпуск кредитной карты
|
|debitCard|Bool|true|Нет|Разрешить выпуск дебетовой карты|

<br>

## SEnvironment

|Параметр|Дефолтное значение|Описание|
|---|:---:|---|
|prod|Да|Стандартное значение, все сервисы в SDK работают в продуктовом режиме|
|sandboxRealBankApp|Нет|Режим песочницы, для авторизации пользователя происходит редирект в приложение Сбербанка. Позволяет протестировать оплату в максимально близких к продуктовым условиях|
|sandboxWithoutBankApp|Нет|Режим песочницы, при авторизации пользователя не осуществляется перехода в приложение Сбербанка. Позволяет производить тестирование на симуляторах и устройствах без SBOL/Сбербанк-онлайн|

<br>

## SPError

####  Класс, служащий для передачи ошибок работы сервисов SDK

|Параметр|Тип|Описание|
|---|:---:|---|
|errorDescription|String|Описание ошибки|

<br>

## SpaymentResult

#### Класс результата выполнения оплаты

|Параметр|Тип|Описание|
|---|:---:|---|
|state|SPayState|Возможные состояния завершения оплаты.<br> Структура [SPayState](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#spaystate)|
|localSessionId|String|Уникальный идентификатор сессии. [Больше информации](https://sdkpay.github.io/SberPaySdkIOSDoc/support#localsessionid)|
|bankInvoiceId|String|Уникальный номер заказа на стороне банка|
|description|String|Описание завершения сценария|

<br>

## SPayState

####  Возможные состояния завершения оплаты

|Возможные состояния|Obj-C|Описание|
|---|:---:|---|
|success|SPayStateSuccess|Оплата успешно произведена|
|waiting|SPayStateWaiting|Оплата производится|
|error|SPayStateError|Во время оплаты произошла ошибка|
|cancel|SPayStateCancel|Оплата прервана пользователем|

<br>

## SPayMethod

#### Сценарии оплаты через SDK

|Параметр|Описание|
|---|---|
|default|Обновленная автоматическая оплата|
|withBankInvoiceId|Автоматическая оплата|
|withBonuses|Оплата со списанием бонусов «Спасибо»|
|withoutRefresh|Оплата без рефреш-токена|
|withPaymentAccount|Оплата с помощью платежных счетов|
|withPartPay|Оплата частями с комиссией|
|withBinding|Оплата с использованием связок|

<br>

## SPaymentRequest

#### Параметры для запуска сценария оплаты через SDK

|Параметр|Тип|Формат|Обязательный|Описание|
|---|:---:|:---:|:---:|---|
|apiKey|String|ANS..512	|Да|Ключ клиента для работы с сервисами платежного шлюза через SDK|
|merchantLogin|String|ANS..512|Да|*Login* партнера для работы с сервисами платежного шлюза|
|language|String|A2|Нет|Уникальный номер (идентификатор) заказа в Платежном шлюзе Банка. Необходимо передавать значение `sbolBankInvoiceId` (передается в `externalParams`)|
|bankInvoiceId|String|ANS..36|Да|Уникальный номер (идентификатор) заказа в Платежном шлюзе Банка. Необходимо передавать значение `sbolBankInvoiceId` (передается в `externalParams`)|
|redirectUri|String|ANS..512|Да|Диплинк, переданный вам вместе c приветственным письмом. Пример: *apptest://spay*|
|orderNumber|String|ANS..36|Да|Уникальный номер (идентификатор) заказа в системе Клиента|
