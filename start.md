# [SberPaySdkIOSDoc](https://sdkpay.github.io/SberPaySdkIOSDoc/)

#### [Бординг](https://sdkpay.github.io/SberPaySdkIOSDoc/boarding) | [Регистрация заказов в платежном шлюзе Сбера](https://sdkpay.github.io/SberPaySdkIOSDoc/order_registration) | [Начало работы](https://sdkpay.github.io/SberPaySdkIOSDoc/start) | [Сценарии оплаты через SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/payment_script) | [Работа в режиме посочницы](https://sdkpay.github.io/SberPaySdkIOSDoc/sandbox_mode) | [Вспомогательные структуры данных](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures) | [Актуальная версия SDK](https://sdkpay.github.io/SberPaySdkIOSDoc/version) | [Поддержка](https://sdkpay.github.io/SberPaySdkIOSDoc/support) | [FAQ](https://sdkpay.github.io/SberPaySdkIOSDoc/faq)

<br>

# Начало работы
> Xcode 13+
> Версия iOS 13.0 и более поздние

<br>

## Реализация сценария

### Настройка info.plist

Для корректной работы SDK в файле **info.plist** приложения должны быть добавлены следующие параметры
```
<key>DTXAutoStart</key>
<string>false</string>
<key>NSAppTransportSecurity</key>
<dict>
  <key>NSExceptionDomains</key>
  <dict>
    <key>gate1.spaymentsplus.ru</key>
    <dict>
      <key>NSExceptionAllowsInsecureHTTPLoads</key>
      <true/>
    </dict>
    <key>ift.gate2.spaymentsplus.ru</key>
    <dict>
      <key>NSExceptionAllowsInsecureHTTPLoads</key>
      <true/>
    </dict>
  </dict>
</dict>
<key>NSFaceIDUsageDescription</key>
<string>Так вы подтвердите, что именно вы выполняете вход</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>Данные о местонахождении собираются и отправляются на сервер для безопасного проведения оплаты</string>
```
> NSLocationWhenInUseUsageDescription - Если у вас уже используется этот параметр, то дублировать его не нужно

<br>

## Подключение SDK к проекту: [spm](https://sdkpay.github.io/SberPaySdkIOSDoc/start#spm) / [cocoapods](https://sdkpay.github.io/SberPaySdkIOSDoc/start#cocoapods) / [бинарный артефакт](https://sdkpay.github.io/SberPaySdkIOSDoc/start#бинарный-артефакт)

### SPM

Перейдите в файл вашего проекта, во вкладке *Package dependencies* нажмите *+* и в строке поиска введите ссылку на репозиторий, переданную вам с договором, и добавьте пакет SDK в свое приложение

### Cocoapods

Для подключения SDK к проекту с помощью cocoapods:
  1. Откройте свой проект в Xcode
  2. Создайте подфайл, запустив `pod init` в терминале или используя меню *File* и выбрав *New File → Podfile*.
  3. Добавьте модули, которые вы хотите использовать, в файл **Podfile**.
  4. Сохраните Podfile и запустите `pod install` в Терминале, чтобы установить модули.
  5. Закройте свой проект в Xcode и откройте файл **.xcworkspace**, созданный после запуска `pod install`.

### Бинарный артефакт

Подключить SDK для успешной работы также можно с помощью [бинарного артефакта](https://github.com/sdkpay/EcomSdkPackage). Перетащите скачанный файл **EcomSdk.xcframework** в *Frameworks, Libraries, and Embedded Content*, а также выставите у зависимости параметр *Embed & Sign*

<br>

## Регистрация deeplink

Для успешной авторизации в среде банка необходим *диплинк*, переданный вам с приветственным письмом. Если вы выпускаете еще одно приложение и публикуете его отдельно - необходимо запросить и получить отдельный диплинк. Если вы используете для нового приложения тот же самый диплинк, при оплате сбол не сможет выбрать нужное приложение для завершения сценария. При добавлении зарегистрированного *диплинка* в **info.plist** пожалуйста убедитесь, что в его составе отсутствует подстрока *://spay*

Выданный Вам диплинк нужно зарегистрировать в файле вашего проекта. Во вкладке *info* необходимо добавить его в раздел *Url types*

<br>

## Имплементация

Импортируйте модуль SPaySdk в проект

### Swift

```
import SPaySdk
```

### Objective-C

```
#import <SPaySdk/SPaySdk.h>
```

<br>

## Инициализация 

В AppDelegate вашего проекта в методе `didFinishLaunchingWithOptions` необходимо реализовать функцию `setup`. Параметры функции представлены [здесь](https://sdkpay.github.io/EcomSdkIOSDoc/data_structures#ecomsdksetupdata)

> Если вы подключили сервис *Плати частями* и пользователь выбрал этот способ для оплаты заказа, то выполняя через back расширенный запрос состояния заказа *getOderStatusExtended.do*, в ответе вы получите значение параметра *paymentWay* равное *BNPL*. Подключить параметр *paymentWay* в callback-уведомлениях возможно в личном кабинете партнера интернет-эквайринга. Это можно сделать в **настройках -> основные настройки -> callback-уведомления**. При заполнении доп. параметров выйдет список всех возможных. Для того, чтобы передавался способ оплаты заказа необходимо выбрать *paymentWay*.  
> Оплаченные частями заказы в личном кабинете партнера интернет-эквайринга будут отмечаться признаком *BNPL* в поле «Платежное средство»  
> При этом денежные средства по заказам, оплаченным частями, поступят от ООО «ЦНФС» («Центр новых финансовых сервисов»), предоставляющей сервис

### Swift

```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: \[UIApplication.LaunchOptionsKey: Any]?) -> Bool {

let window = UIWindow(frame: UIScreen.main.bounds)

self.window = window

  SPay.setup(bnplPlan: true,
             resultViewNeeded: true,
             helpers: true,
             needLogs: true,
             helperConfig: SBHelperConfig(sbp: true,
                                          creditCard:true),
             environment: .prod) { error in
            if let error {
                // Ошибка инициализации SDK
            }
        }

return true
}
```

### Objective-C

```
-   (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

SConfig *config = [[SConfig alloc] initWithSbp:true creditCard:true debitCard:true];

     [SPay setupWithBnplPlan:true
                    helpers:true
               helperConfig: config
                environment: SEnvironmentProd
                  completion:nil];

return YES;

}
```

После чего необходимо реализовать в `AppDelegate` вашего проекта метод `getAuthURL` как показано ниже. Вместо `sberPayExampleapp` используйте свой диплинк, переданный вам вместе с приветсвенным письмом.

### Swift

```
func application(_ app: UIApplication,

open url: URL,

options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {

if url.scheme == "sberPayExampleapp" && url.host == "spay" {

SPay.getAuthURL(url)

}

return true

}
```

### Objective-C

```
-   (BOOL)application:(UIApplication *)app

openURL:(NSURL *)url

options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> )options {

if ([url.scheme isEqualToString:@"sberPayExample.app"] && [url.host isEqualToString:@"spay"])

{

[SPay getAuthURL: url];

}

return YES;

}
```

> Если в Вашем проекте используется `SceneDelegate`, то вы должны использовать вместо `func application(_ app: UIApplication, open url: URL,..` метод, описанный ниже, в классе `SceneDelegate`

```
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    if let url = URLContexts.first?.url, url.scheme == "sberPayExample.app" && url.host == "spay" {
        SPay.getAuthURL(url)
    }
}
```

### Helpers

Helpers или помогашки - функционал, позволяющий клиенту с недостаточным количеством средств быстро пополнить счет или выпустить новые продукты для оплаты.  
Структура [SBHelperConfig](https://sdkpay.github.io/SberPaySdkIOSDoc/data_structures#sbhelperconfig)

<br>

## Проверка готовности оплаты

Для проверки готовности сервисов SberPay к оплате необходимо вызывать метод `isReadyForSPay`

```
SPay.isReadyForSPay
```

Если сервисы готовы, то метод вернет ответ *true*, и можно будет отрисовать кнопку оплаты

<br>

## Отзыв рефреш-токена

Для отзыва токена необходимо воспользоватся методом `logout`. Этот метод удаляет локально сохраненный рефреш-токен, если он присутствует

> Необходимо вызвать этот метод при разлогине пользователя в своем приложении

### Swift

```
SPay.logout()
```

### Objective-C

```
[SPay logout];
```

<br>

## Отрисовка кнопки оплаты

Для вызова метода оплаты можно использовать готовый класс кнопки `SBPButton` или *отрисовать кнопку самостоятельно* в соответсвии с [гайдлайнами](https://cdn-app.sberdevices.ru/misc/0.0.0/assets/bsm-docs/button-guideline-ios.pdf)

Процесс инициализации кнопки оплаты `SBPButton`:

### Swift

```
let button = SBPButton()
button.tapAction = { ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣

// обработка нажатия ⁣

}
```

### Objective-C

```
SPButton button = [[SBPButton alloc] init]; ⁣
⁣button.tapAction = \^{ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣ ⁣⁣ ⁣

// обработка нажатия ⁣

};
```