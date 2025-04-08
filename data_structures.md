# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

# Вспомогательные структуры данных

## EcomSdkSetupData

#### Параметры для передачи в функцию `setup`

|Параметр|Тип|Дефолтное значение|Обязательный|Описание|
|---|:---:|:---:|:---:|---|
|bnplPlan|Bool|true|Нет|Функционал «Оплата частями»|
|helpers|Bool|true|Нет|Функционал Helpers (Помогашки)|
|resultViewNeeded|Bool|true|Нет|Отображение экранов со статусом|
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

|Значение|Дефолтное значение|Описание|
|---|:---:|---|
|prod|Да|Стандартное значение, все сервисы в SDK работают в продуктовом режиме|
|sandboxRealBankApp|Нет|Режим песочницы, для авторизации пользователя происходит редирект в приложение Сбербанка. Позволяет протестировать оплату в максимально близких к продуктовым условиях|
|sandboxWithoutBankApp|Нет|Режим песочницы, при авторизации пользователя не осуществляется перехода в приложение Сбербанка. Позволяет производить тестирование на симуляторах и устройствах без SBOL/Сбербанк-онлайн|

<br>

## SPError

####  Класс, служащий для передачи ошибок работы сервисов SDK

|Объект|Тип|Описание|
|---|:---:|---|
|errorDescription|String|Описание ошибки|

<br>

## SPayState

#### Класс, служащий для передачи состояния оплаты

|Возможные состояния|Obj-C|Описание|
|---|:---:|---|
|success|SPayStateSuccess|Оплата успешно произведена|
|waiting|SPayStateWaiting|Оплата производится|
|error|SPayStateError|Во время оплаты произошла ошибка|
