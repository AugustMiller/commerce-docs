# Events

Commerce emits a number of events, which enable developers to extend or modify behaviors. Be sure to familiarize yourself with the [Craft 3 events documentation] before digging in.

Below, the available events are divided into conceptual groups, so adjacent items may not be documented within the same class. For a complete, up-to-date list, view the source of the relevant Commerce _Elements_, _Models_, and _Services_.

## Orders
- `commerce\elements\Order::EVENT_BEFORE_COMPLETE_ORDER`
- `commerce\elements\Order::EVENT_AFTER_COMPLETE_ORDER`
- `commerce\services\OrderHistories::EVENT_ORDER_STATUS_CHANGE`
- `commerce\services\OrderStatuses::EVENT_DEFAULT_ORDER_STATUS`

### PDFs
- `commerce\services\Pdf::EVENT_BEFORE_RENDER_PDF`
- `commerce\services\Pdf::EVENT_AFTER_RENDER_PDF`

## Line Items
- `commerce\elements\Order::EVENT_AFTER_ADD_LINE_ITEM`
- `commerce\services\LineItems::EVENT_BEFORE_SAVE_LINE_ITEM`
- `commerce\services\LineItems::EVENT_AFTER_SAVE_LINE_ITEM`
- `commerce\services\LineItems::EVENT_CREATE_LINE_ITEM`
- `commerce\services\LineItems::EVENT_POPULATE_LINE_ITEM`

## Products
Products are just a wrapper around the Craft `Element`, so they will emit all `Element` events. When using these events, be sure to filter out  the noise of other elements, by checking its type:

```php
use craft\services\Elements;
use craft\commerce\elements\Product;

Event::on(Elements::class, Elements::EVENT_BEFORE_SAVE_ELEMENT, function ($event) {
    if (is_a($element, Product::class) {
        // $element is a Product, and you can treat it as such!
    }
});
```

### Types
- `commerce\services\Products::EVENT_BEFORE_SAVE_PRODUCTTYPE`
- `commerce\services\Products::EVENT_AFTER_SAVE_PRODUCTTYPE`

## Variants
Variants are also a type of `Purchasable` (see below), and in turn, an Element, so the note about products applies here, as well:

```php
use craft\services\Elements;
use craft\commerce\elements\Variant;

Event::on(Elements::class, Elements::EVENT_BEFORE_SAVE_ELEMENT, function ($event) {
    if (is_a($element, Variant::class) {
        // $element is a Variant, and you can treat it as such!
    }
});
```

## Purchasables (Abstract)
- `commerce\services\Purchasables::EVENT_REGISTER_PURCHASABLE_ELEMENT_TYPES`

## Subscriptions
- `commerce\services\Subscriptions::EVENT_EXPIRE_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_BEFORE_CREATE_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_AFTER_CREATE_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_BEFORE_REACTIVATE_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_AFTER_REACTIVATE_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_BEFORE_SWITCH_SUBSCRIPTION_PLAN`
- `commerce\services\Subscriptions::EVENT_AFTER_SWITCH_SUBSCRIPTION_PLAN`
- `commerce\services\Subscriptions::EVENT_BEFORE_CANCEL_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_AFTER_CANCEL_SUBSCRIPTION`
- `commerce\services\Subscriptions::EVENT_BEFORE_UPDATE_SUBSCRIPTION` (There is not currently an `AFTER` event for Subscription updates)
- `commerce\services\Subscriptions::EVENT_RECEIVE_SUBSCRIPTION_PAYMENT`

### Plans
- `commerce\services\Plans::EVENT_ARCHIVE_PLAN`
- `commerce\services\Plans::EVENT_BEFORE_SAVE_PLAN`
- `commerce\services\Plans::EVENT_AFTER_SAVE_PLAN`

## Payments
- `commerce\services\Payments::EVENT_AFTER_PAYMENT_TRANSACTION`
- `commerce\services\Payments::EVENT_BEFORE_CAPTURE_TRANSACTION`
- `commerce\services\Payments::EVENT_AFTER_CAPTURE_TRANSACTION`
- `commerce\services\Payments::EVENT_BEFORE_REFUND_TRANSACTION`
- `commerce\services\Payments::EVENT_AFTER_REFUND_TRANSACTION`
- `commerce\services\Payments::EVENT_BEFORE_PROCESS_PAYMENT_EVENT`
- `commerce\services\Payments::EVENT_AFTER_PROCESS_PAYMENT_EVENT`
- `commerce\services\PaymentSources::EVENT_DELETE_PAYMENT_SOURCE`
- `commerce\services\PaymentSources::EVENT_BEFORE_SAVE_PAYMENT_SOURCE`
- `commerce\services\PaymentSources::EVENT_AFTER_SAVE_PAYMENT_SOURCE`

### Transactions
- `commerce\services\Transactions::EVENT_AFTER_SAVE_TRANSACTION`
- `commerce\services\Transactions::EVENT_AFTER_CREATE_TRANSACTION`

## Addresses
- `commerce\models\Address::EVENT_REGISTER_ADDRESS_VALIDATION_RULES`
- `commerce\services\Addresses::EVENT_BEFORE_SAVE_ADDRESS`
- `commerce\services\Addresses::EVENT_AFTER_SAVE_ADDRESS`

## Adjustments
- `commerce\services\OrderAdjustments::EVENT_REGISTER_ORDER_ADJUSTERS`

### Discounts + Sales
- `commerce\services\Discounts::EVENT_BEFORE_MATCH_LINE_ITEM`
- `commerce\services\Sales::EVENT_BEFORE_MATCH_PURCHASABLE_SALE`

### Shipping
- `commerce\services\ShippingMethods::EVENT_REGISTER_AVAILABLE_SHIPPING_METHODS`

## Emails
- `commerce\services\Emails::EVENT_BEFORE_SEND_MAIL`
- `commerce\services\Emails::EVENT_AFTER_SEND_MAIL`

## Gateways
- `commerce\services\Gateways::EVENT_REGISTER_GATEWAY_TYPES`
