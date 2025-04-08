# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

<br>

# Работа в режиме песочницы

> В данном режиме не отображаются настоящие данные клиента

Песочница - режим работы SDK, который необходим для отладки процесса оплаты. В режиме песочницы есть возможность пройти весь процесс оплаты через SDK в Вашем приложении без регистрации реальных заказов. Это можно реализовать двумя способами.  
Рассмотрите первый простой вариант, он подойдет для тех, кто не интегрирован с платежным шлюзом Банка и ищет способ протестировать визуальную составляющую продукта. Реализуете сценарий «Оплата вне SDK».  
Если вы интегрированы с платежным шлюзом Сбера, то мы рекомендуем второй вариант - использовать идентификаторы заказов в Платежном шлюзе Банка из тестового окружения. Обратите внимание, что в зависимости от того, с какой именно версией протокола вы интегрированы могут потребоваться отдельные учетные данные для регистрации заказов

<br>

## Необходимые данные для тестирования

Для получения доступа к песочнице Вам необходимо отправить запрос на почту *support@ecom.sberbank.ru*. В теме письма обязательно указать "Получение доступа к песочнице Sandbox SDK SberPay In-App"

<br>

## Реализация в коде

В методе `setup` передайте в параметр `environment` одно из возможных значений класса [SEnvironment](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#senvironment)

Пример кода:

### Swift

```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: \[UIApplication.LaunchOptionsKey: Any]?) -> Bool {

let window = UIWindow(frame: UIScreen.main.bounds)

self.window = window

 SPay.setup(apiKey: "", bnplPlan: true, environment: .sandboxRealBankApp)

return true

}
```

### Objective-C

```
-   (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

[SPay setupWithApiKey:@"" bnplPlan:true environment: SEnvironmentProd completion:nil];

return YES;

}
```