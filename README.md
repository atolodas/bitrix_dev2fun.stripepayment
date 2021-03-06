# Платежный модуль Stripe

Модуль позволяет начать принимать оплату через платежную систему Stripe.

### Способы оплаты

* Банковские карты (Card)
* Sepa Debit / IBAN
* Sofort
* Giropay

## Инструкция

1. Узнать используемую кодировку (dbconn.php или after_connect_d7.php или after_connect.php)
1. Проверить права у папки modules
1. Скопировать файлы из нужной папки репозитория (utf8 или win1251) на свой сервер в папку /bitrix/modules/
1. Перейти в административную панель
1. Установить модуль в административной панели.
1. Прочитать сообщение
1. Зайти в Магазин -> Настройки -> Платежные системы -> Добавить платежную систему
1. В пункте "Обработчик", выбираем stripe.
1. В полях ниже указываем свои данные
1. Поблагодарить автора :)
1. Использовать.


## Поддержка режимов:
* тестовый режим (demo mode) - по умолчанию
* боевой режим (live mode)

## Поддержка шаблонов:
* **POPUP** - выводится кнопка, при нажатии появляется дефолтное окно stripe
* **CUSTOM** - выводится форма, с поддержкой card, Sepa Debit/IBAN, Sofort, Giropay

Куда ложить свой шаблон?

_Вы можете создать свой шаблон вывода и в последующем выбрать его в настройках._

Вам нужно положить свой шаблон в одну из нижеследующих каталогов (пути от корня сайта):
* `/local/php_interface/sale_payment/stripe/templates/`
* `/bitrix/php_interface/sale_payment/stripe/templates/`

_Последовательность соблюдена._\
_Совпадения имен игнорируются._

## Поддержка событий:

* **OnBeforeStripeCharge** - вызывается после создания customer.\
**Передаются параметры:**
    * `&$arCreateFields` - массив, который дальше идет в `\Stripe\Charge::create`
    * `$customer` - объект от `\Stripe\Customer::create`
    
* **OnBeforeUpdateOrder** - вызывается после получения статуса оплаты.\
Передаются параметры:
    * `&$arFields` - массив полей, который идет в обновление заказа (`CSaleOrder::Update`)
    * `$charge` - объект от `\Stripe\Charge::create`
    * `$orderID` - идентификатор заказа
    
* **OnBeforeSuccessOutput** - вызывается перед выводом сообщения о успехе.\
Передаются параметры:
    * `&$output` - строка или HTML-код, которая выведет результат.
    * `$arFields` - массив полей от заказа (тот же, что был в `CSaleOrder::Update`)
    * `$orderID` - идентификатор заказа
    
* **OnBeforeErrorOutput** - вызывается перед выводом сообщения об ошибке.\
Передаются параметры:
    * `&$error` - строка или HTML-код, которая выведет ошибку.
    * `$errorText` - строка с сообщением ошибки
    * `$arFields` - массив полей от заказа (тот же, что был в `CSaleOrder::Update`)
    * `$orderID` - идентификатор заказа
Если есть нарекания или предложения по улучшению модуля пишите на почту техподдержки.