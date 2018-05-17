<p align="center"><img src="https://seeklogo.com/images/S/slack-logo-DE4445077C-seeklogo.com.png" height="60px"><img src="https://laravel.com/assets/img/components/logo-laravel.svg" height="60px"></p>

<p align="center">
<a href="https://travis-ci.com/gpressutto5/laravel-slack"><img src="https://img.shields.io/travis/gpressutto5/laravel-slack/master.svg?style=for-the-badge" alt="Build Status"></a>
<a href="https://codecov.io/gh/gpressutto5/laravel-slack"><img src="https://img.shields.io/codecov/c/github/gpressutto5/laravel-slack/master.svg?style=for-the-badge" alt="codecov"></a>
<a href="https://packagist.org/packages/gpressutto5/laravel-slack"><img src="https://img.shields.io/packagist/v/gpressutto5/laravel-slack.svg?style=for-the-badge" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/gpressutto5/laravel-slack"><img src="https://img.shields.io/packagist/php-v/gpressutto5/laravel-slack.svg?style=for-the-badge" alt="PHP from Packagist"></a>
<a href="https://packagist.org/packages/gpressutto5/laravel-slack"><img src="https://img.shields.io/badge/laravel-%3E%3D5.5-orange.svg?style=for-the-badge" alt="Laravel Version"></a>
<a href="https://packagist.org/packages/gpressutto5/laravel-slack"><img src="https://img.shields.io/packagist/dt/gpressutto5/laravel-slack.svg?style=for-the-badge" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/gpressutto5/laravel-slack"><img src="https://img.shields.io/packagist/l/gpressutto5/laravel-slack.svg?style=for-the-badge" alt="License"></a>
<br>
Based on <a href="https://github.com/illuminate/mail">illuminate/mail</a>
</p>

## About Laravel Slack

Slack notification for Laravel as it should be.
Since it uses On-Demand Notifications, it requires Laravel 5.5 or higher.

## Installation 

Require this package in your composer.json and update your dependencies:

```bash
composer require gpressutto5/laravel-slack
```

Since this package supports Laravel's Package Auto-Discovery
you don't need to manually register the ServiceProvider.

After that, publish the configuration file:

```bash
php artisan vendor:publish --provider="Pressutto\LaravelSlack\ServiceProvider"
```

You're gonna need to configure an ["Incoming Webhook"](https://api.slack.com/incoming-webhooks) integration for your Slack team.

## Configuration

On the published configuration file `config/laravel-slack.php`
you can change options like the Webhook URL, the default channel,
the application name and the application image.

For security reasons you shouldn't commit your Webhook URL,
so this package will, by default, use the environment variable
`SLACK_WEBHOOK_URL`. You can just add it to your `.env` file.
Like this:

```dotenv
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/XXXXXXXXX/XXXXXXXXX/XXXXXXXXXXXXXXXXXXXXXXXX
```

## Usage

You can send simple Slack messages like this:

- Send message to a channel:

```php
\Slack::to('#finance')->send('Hey, finance channel! A new order was created just now!');
```

- Send message to an user:

```php
\Slack::to('@joe')->send("Hey Joe! It looks like you've forgotten your password! Use this token to recover it: as34bhdfh");
```

- Send message to multiple users:

```php
\Slack::to(['@zoe', '@amy', '@mia'])->send('I swear, honey, you are the only one... :heart:');
//         ↑  look at this array  ↑
```

- Mix it up:

```php
\Slack::to('#universe', '@god', '#scientists')->send(':thinking_face:');
//         ↑ what? I don't need that array? ↑
```

- No recipient:

```php
\Slack::send('Default message to the default channel, set on config/laravel-slack.php.');
```

- Send SlackMessage objects:

```php
class HelloMessage extends SlackMessage
{
    public $content = "Hey bob, I'm a sending a custom SlackMessage";
    public $channel = '@bob';
}
\Slack::send(new SlackMessage());
```

- And more...

    This package is both under development and underdeveloped.
    Many features will come. Stay tuned and, please, help us!
