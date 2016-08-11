# Pusher push notifications channel for Laravel 5.3 [WIP]

[![Latest Version on Packagist](https://img.shields.io/packagist/v/laravel-notification-channels/pusher-push-notifications.svg?style=flat-square)](https://packagist.org/packages/laravel-notification-channels/pusher-push-notifications)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Build Status](https://img.shields.io/travis/laravel-notification-channels/pusher-push-notifications/master.svg?style=flat-square)](https://travis-ci.org/laravel-notification-channels/pusher-push-notifications)
[![StyleCI](https://styleci.io/repos/65379321/shield)](https://styleci.io/repos/65379321)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/9015691f-130d-4fca-8710-72a010abc684.svg?style=flat-square)](https://insight.sensiolabs.com/projects/9015691f-130d-4fca-8710-72a010abc684)
[![Quality Score](https://img.shields.io/scrutinizer/g/laravel-notification-channels/pusher-push-notifications.svg?style=flat-square)](https://scrutinizer-ci.com/g/laravel-notification-channels/pusher-push-notifications)
[![Total Downloads](https://img.shields.io/packagist/dt/laravel-notification-channels/pusher-push-notifications.svg?style=flat-square)](https://packagist.org/packages/laravel-notification-channels/pusher-push-notifications)

This package makes it easy to send [Pusher push notifications](https://pusher.com/docs/push_notifications) with Laravel 5.3.

## Installation

You can install the package via composer:

``` bash
composer require laravel-notification-channels/pusher-push-notifications
```

You must install the service provider:

```php
// config/app.php
'providers' => [
    ...
    NotificationChannels\PusherPushNotifications\Provider::class,
];
```

## Usage

Now you can use the channel in your `via()` method inside the notification as well as send a push notification:

``` php
use NotificationChannels\PusherPushNotifications\Channel;
use NotificationChannels\PusherPushNotifications\Message;
use Illuminate\Notifications\Notification;

class AccountApproved extends Notification
{
    public function via($notifiable)
    {
        return [Channel::class];
    }

    public function toPushNotification($notifiable)
    {
        return (new Message())
            ->iOS()
            ->badge(1)
            ->sound('success')
            ->body("Your {$notifiable->service} account was approved!");
    }
}
```

### Setting up your Pusher account

- Login to https://dashboard.pusher.com/
- Select your app from the sidebar or create a new app.
- Click on the "Push Notifications" tab.
- Upload your APNS Certificate or add your GCM API key.
- Now select the "App Keys" tab.
- Copy your `app_id`, `key`, and `secret`.
- Update the values in your `config/broadcasting.php` file under the pusher connection.
- You're now good to go.


## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing
    
``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email theMohamedSaid@gmail.com instead of using the issue tracker.

## Credits

- [Mohamed Said](https://github.com/themsaid)
- [Marcel Pociot](https://github.com/mpociot)
- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
