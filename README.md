# Kirby Maintenance Mode Plugin

This plugin uses the `route:before` hook to hide the whole website from not-logged-in users when `option('maintenance')` is set to `true`. It also sends a `503` code.

Kirby urls like `assets`, `api`, `media`, `panel` will be ignored and are still available.

## Installation

```bash
composer require moritzebeling/kirby-maintenance
composer update moritzebeling/kirby-maintenance
```

Or download/clone this repo into `site/plugins` of your Kirby project.

There are different ways to control the maintenance mode:

## Via option

```php
// site/config.php
return [
    // one line switch
    'maintenance' => true,

    // more detailed configuration
    'moritzebeling.kirby-maintenance' => [
        'ignore' => [],
        'css' => false,
        'text' => 'This website is currently under maintenance and will be back online soon.',
        'allowed-users' => []
    ]
];
```

## Via panel

Add a field `maintenance` to the `site.yml` blueprint to meet the condition `$site->maintenance()->isTrue()`.

Via `$site->maintenance_text()` you could edit the text that would welcome any logged out website visitor.

You can also use one of the prefabricated blueprint parts:

- `tabs/maintenance`
- `sections/maintenance`
- `fields/maintenance`
- `fields/maintenance_text`

## Via file

You could also add a `/.maintenance` file to the Kirby root directory to switch on maintenance mode. This method is used by [bnomei/kirby3-janitor](https://github.com/bnomei/kirby3-janitor) plugin. If you enter any text inside that file, this will be the output when the site is in maintenance mode.

Suggested by https://github.com/moritzebeling/kirby-maintenance/issues/1

## Allow page-access only to certain users

With the `moritzebeling.kirby-maintenance.allowed-users`option you allow access only to certain users, e.g. for the development-team to check changes before allowing access to the content-team

```php
// site/config.php
return [
    // one line switch
    'maintenance' => true,

    // more detailed configuration
    'moritzebeling.kirby-maintenance' => [
      'allowed-users' => env('KIRBY_MAINTENANCE_ALLOWED_USERS') ? explode(',', env('KIRBY_MAINTENANCE_ALLOWED_USERS')) : []
    ]
```

```dotenv
# .env
KIRBY_MAINTENANCE_ALLOWED_USERS=deployer1@develop.team,deployer2@develop.team
```

## Add style

With the `moritzebeling.kirby-maintenance.css` option you could add a stylesheet, e.g.:

```css
/* /assets/css/maintenance.css */
body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 1rem;
    display: flex;
    text-align: center;
    justify-content: center;
    align-items: center;
}
.message {
    max-width: 500px;
}
```

## Development

1. Install a fresh Kirby StarterKit
2. `cd site/plugins`
3. `git clone` this repo

Roadmap
- [ ] Check if there is a page with the slug `maintenance`, if yes, display that page
- [ ] Allow pages to be ignored via field or blueprint option
- [ ] Multilang support

## ☕️ Support

If you like this plugin, I would be glad if you would invite for on a coffee via [PayPal](http://more.moritzebeling.com/support)
If you have any ideas for further development or stumble upon any problems, please open an issue or PR. Thank you!

## Warranty

This plugin is work in progress and comes without any warranty. Use at your own risk.