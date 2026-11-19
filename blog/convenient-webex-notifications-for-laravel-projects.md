---
type: Article
title: Convenient Webex Notifications for Laravel Projects
canonical_url: https://developer.webex.com/blog/convenient-webex-notifications-for-laravel-projects
content_type: blog
date: '2022-03-29'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/convenient-webex-notifications-for-laravel-projects)

[Laravel](https://laravel.com/docs/10.x) is the most popular backend web framework with over 72k Stars on GitHub that boasts an expressive, elegant syntax and a vibrant ecosystem of projects. One such project is [Laravel Notifications](https://laravel.com/docs/10.x/notifications), which simplifies 
sending notifications across a variety of delivery channels such as database and email. Although out-of-the-box such 
support is limited to only a handful of channels, community-driven 
[Laravel Notification Channels](https://packagist.org/explore/?query=laravel-notification-channels%2F) can 
easily extend compatibility to others, including [Webex](https://web.webex.com).

That is an exciting development since Laravel based projects can use this single, consistent interface to send notifications 
through Webex in addition to already supported channels like Telegram, Twitter, Facebook, and many more! You can find the 
complete list of supported channels on the project's website 
[https://laravel-notification-channels.com/about](https://laravel-notification-channels.com/about). The project currently 
supports more than 50 channels.


### Installation

If you are already familiar with Laravel Notifications, follow the steps below to use the new Laravel Notification Channels Webex package.

#### Add the package

Add the package as a project dependency using Composer:


```bash
composer require laravel-notification-channels/webex
```

#### Add a new service configuration

You will also need to include a Webex service configuration to your application. To do this, edit
the `config/services.php` file and add the following:

```php
'webex' => [
    'notification_channel_url' => env('WEBEX_NOTIFICATION_CHANNEL_URL', 'https://webexapis.com/v1/messages'),
    'notification_channel_id' => env('WEBEX_NOTIFICATION_CHANNEL_ID'),
    'notification_channel_token' => env('WEBEX_NOTIFICATION_CHANNEL_TOKEN')
],
```

Then use the `WEBEX_NOTIFICATION_CHANNEL_ID` and `WEBEX_NOTIFICATION_CHANNEL_TOKEN`
[environment variables](https://laravel.com/docs/10.x/configuration#environment-configuration)
to define your Webex ID and Token. One way to get these values is by creating a new
[Webex Bot](https://developer.webex.com/my-apps/new/bot).


### Usage

If you are new to Laravel Notification, I highly recommend reading the official documentation which
goes over the basics of [generating](https://laravel.com/docs/9.x/notifications#generating-notifications)
and [sending](https://laravel.com/docs/10.x/notifications#sending-notifications) notifications.
The guide below assumes that you have successfully generated a notification class with a
[`via`](https://laravel.com/docs/10.x/notifications#specifying-delivery-channels) method whose return value 
includes `'webex'` or `NotificationChannels\Webex\WebexChannel::class`. For example:

```php
<?php
 
namespace App\Notifications;
 
use Illuminate\Bus\Queueable;
use Illuminate\Notifications\Notification;
use NotificationChannels\Webex\WebexChannel;
 
class InvoicePaid extends Notification
{
    use Queueable;
 
    // ...
    
    /**
     * Get the notification's delivery channels.
     *
     * @param  mixed  $notifiable
     * @return array
     */
    public function via($notifiable)
    {
        return [WebexChannel::class];
    }
    
    // ...
}
```

#### Formatting Webex Notifications

If a notification supports being sent as a Webex message, you should define a `toWebex`
method on the notification class. This method will receive a `$notifiable` entity and should return
a `\NotificationChannels\Webex\WebexMessage` instance. Webex messages may contain text content 
as well as at most one file or an attachment (for [buttons and cards](https://developer.webex.com/buttons-and-cards-designer)). 

Let's take a look at a sample `toWebex` example, which we could add to our `InvoicePaid` class
[above](#usage).

```php
/**
 * Get the Webex Message representation of the notification.
 *
 * @param  mixed  $notifiable
 * @return \NotificationChannels\Webex\WebexMessage
 *
 * @throws \NotificationChannels\Webex\Exceptions\CouldNotCreateNotification
 */
public function toWebex($notifiable)
{
    return (new WebexMessage)
        ->text('Invoice Paid!')
        ->markdown('# Invoice Paid!')
        ->file(function (WebexMessageFile $file) {
            $file->path('storage/app/invoices/uwnQ0uAXzq.pdf')
                ->name('invoice.pdf');
        });
}
```

#### Routing Webex Notifications

To route Webex notifications to the proper Webex user or room/space, define a
`routeNotificationForWebex` method on your notifiable entity. This should return a Webex registered
email address or a Webex HTTP API resource identifier for a user or room/space to which the
notification should be delivered.

```php
<?php
 
namespace App\Models;
 
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
 
class User extends Authenticatable
{
    use Notifiable;
 
    /**
     * Route notifications for the Webex channel.
     *
     * @param  \Illuminate\Notifications\Notification  $notification
     * @return string
     */
    public function routeNotificationForWebex($notification)
    {
        if (!empty($this->email)) {             // a Webex registered email address
            return $this->email;
        } else if (!empty($this->personId)) {   // a Webex HTTP API resource identifier for a user
            return $this->personId;
        } else if (!empty($this->roomId)) {     // a Webex HTTP API resource identifier for a room/space
            return $this->roomId;
        }

        return null;                            // don't route notification for Webex channel
    }
}
```

### Wrapping Up
This article provided a brief overview of the new Laravel Notification Channels Webex package. Laravel project owners 
are encouraged to use this package to simplify their workload when sending notification via Webex. To see other such 
community offerings or learn more about our developer platform, please visit [Webex Developers](https://developer.webex.com/docs).
