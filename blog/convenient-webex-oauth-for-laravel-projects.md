---
type: Article
title: Convenient Webex OAuth for Laravel Projects
canonical_url: https://developer.webex.com/blog/convenient-webex-oauth-for-laravel-projects
content_type: blog
date: '2021-11-17'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/convenient-webex-oauth-for-laravel-projects)

[Laravel](https://laravel.com/docs/10.x) is the most popular backend web framework with over 72k Stars on GitHub that boasts an expressive, elegant syntax and a vibrant ecosystem of projects. One such project is [Laravel Socialite](https://laravel.com/docs/10.x/socialite), which simplifies authenticating with OAuth providers, enabling a third-party application to access an HTTP service. Although out-of-the-box such support is limited to only a handful of platforms, community-driven [Socialite Providers packages](https://packagist.org/packages/socialiteproviders/providers?query=socialiteproviders%2F) can easily extend compatibility to others, including [Webex](https://web.webex.com). 

That is an exciting development since Laravel based projects can use this single, consistent interface to authenticate with Webex in addition to already supported platforms like Microsoft Azure, Auth0, Bitbucket, GitHub, Strava, Telegram, and many more! You can find the complete list of supported platforms on the project's website https://socialiteproviders.com/about. The project currently supports more than 60 platforms.

### Installation

If you are already familiar with Laravel Socialite, follow the steps below to use the new Socialite Providers Webex package.

#### Add the package

Add the package as a project dependency using Composer:

```bash
composer require socialiteproviders/webex
```

#### Add a new service configuration

You will also need to include a Webex service configuration to your application. To do this, edit the `config/services.php` file and add the following:

```php
'webex' => [
  'client_id' => env('WEBEX_CLIENT_ID'),
  'client_secret' => env('WEBEX_CLIENT_SECRET'),
  'redirect' => env('WEBEX_REDIRECT_URI')
],
```

#### Add a new service provider

- Remove `Laravel\Socialite\SocialiteServiceProvider` from your `providers[]` array in `config\app.php` if you have added it already.
- Add `\SocialiteProviders\Manager\ServiceProvider::class` to your `providers[]` array in `config\app.php`.

For example:

```php
'providers' => [
    // a whole bunch of providers
    // remove 'Laravel\Socialite\SocialiteServiceProvider',
    \SocialiteProviders\Manager\ServiceProvider::class, // add

];
```

#### Add a provider event listener

Configure the package's listener to listen for `SocialiteWasCalled` events.

Add the event to your `listen[]` array in `app/Providers/EventServiceProvider`:

```php
protected $listen = [
    \SocialiteProviders\Manager\SocialiteWasCalled::class => [
        // ... other providers
        'SocialiteProviders\\Webex\\WebexExtendSocialite@handle',
    ],
];
```

See the [Base Installation Guide](https://socialiteproviders.com/usage/) for detailed instructions.

### Usage

You should now be able to use the provider like you would regularly use [Socialite](https://laravel.com/docs/10.x/socialite) (assuming you have the facade installed):

```php
return Socialite::driver('webex')->redirect();
```

#### Returned User fields

The following user fields are returned:

- `id`
- `nickname` (may be `null`)
- `name` (may be `null`)
- `first_name` (may be `null`)
- `last_name` (may be `null`)
- `email`
- `avatar` (may be `null`)

<br/>

### Wrapping Up

This article provided a brief overview of the new Socialite Providers Webex package. Laravel project owners are encouraged to use this package to simplify their workload when authenticating with Webex. To see other such community offerings or learn more about our developer platform, please visit [Webex Developers](https://developer.webex.com/docs/).
