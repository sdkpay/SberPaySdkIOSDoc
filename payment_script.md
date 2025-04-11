# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

<br>

# Сценарий оплаты

## Схема взаимодействия

<img src="docs/assets/img/auto-alg.png" width="600">

<br>

## Доступные сценарии оплаты

В SDK представлены следующие сценарии оплаты:
- Обновленная автоматическая оплата
- Автоматическая оплата
- Оплата со списанием бонусов «Спасибо»
- Оплата без рефреш-токена
- Оплата с помощью платежных счетов
- Оплата частями с комиссией
- Оплата с использованием связок

<br>

## Реализация сценария оплаты

> На данном этапе в SDK был введен универсальный метод вызова оплаты - `pay`, который заменяет под собой все предыдущие способы оплаты.  
В ближайшее время планируется оставить только новый метод оплаты `pay`, старые методы оплаты будут удалены из SDK. На данный момент они уже помечены как *Deprecated*

Для проведения необходимого для Вас сценария оплаты надо передать в метод `pay` структуру [SPayMethod](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#spaymethod), а также структуру с параметрами [SPaymentRequest](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#spaymentrequest)

Пример реализации структуры запроса:

### Swift

```
let request = SPaymentRequest(
    apiKey: "Your API key",
    bankInvoiceId: bankInvoiceId,
    orderNumber: "Your order number",
    merchantLogin: "Test shop",
    redirectUri: "sberPayExampleapp://spay"
    )

SPay.pay(view: self,
         method: method,
         request: request) { state, bankInvoiceId, localSessionId, info in
    
    switch state {
        case .success: print("Успешный результат")
        case .waiting: print("Необходимо проверить статус оплаты")
        case .cancel: print("Пользователь отменил оплату")
        case .error: print("(info) - описание ошибки")
        @unknown default: print("Неопределенная ошибка")
    }
}
```

### Objective-C

```
SPaymentRequest *request = [[SPaymentRequest alloc] initWithapiKey: @"Your API key"
bankInvoiceId:@"12312312"
orderNumber:@"123add"
merchantLogin:@"Test shop"
redirectUri:@"sberPayExampleapp://spay",
bindingId:nil];

[SPay payWith:self method: method with:request completion:^(enum SPayState state, NSString * _Nonnull bankInvoiceId, NSString * _Nonnull localSessionId, NSString * _Nonnull info) {

switch(state) {
    case SPayStateSuccess: NSLog(@"Успешный результат");
    break;
    case SPayStateWaiting: NSLog(@"Необходимо проверить статус оплаты");
    break;
    case SPayStateCancel: NSLog(@"Пользователь отменил оплату");
    break;
    case SPayStateError: NSLog(@"%@ - описание ошибки", info);
    break;
}
}];
```
