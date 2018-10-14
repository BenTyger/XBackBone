
# XBackBone 📤 [![Build Status](https://travis-ci.org/SergiX44/XBackBone.svg?branch=master)](https://travis-ci.org/SergiX44/XBackBone)
XBackBone is a simple, self-hosted, lightweight PHP backend for the instant sharing tool ShareX. It supports uploading and displaying images, GIF, video, code, formatted text, and file downloading and uploading. Also have a web UI with multi user management and past uploads history.

## Features

+ Supports every upload type from ShareX.
+ Code uploads syntax highlighting.
+ Video uploads player.
+ Files upload download page.
+ User management, multi user features and roles.
+ Public and private uploads.
+ Web UI for each user.
+ Logging system.
+ Auto config generator for ShareX.
+ Share to Telegram.

## How to Install
XBackBone require PHP >= `7.1`, writable storage path and PDO, with installed the required extensions (ex. `php-sqlite3` for SQLite, `php-gd` and `php-json`):

+ **[release, stable]** Download latest release from GitHub: [Latest Release](https://github.com/SergiX44/XBackBone/releases/latest)
+ Extract the release zip to your document root.
+ Edit the config file:
```sh
cp config.example.php config.php
```
By default, XBackBone will use Sqlite3 as DB engine, and a `storage` dir in the main directory. You can leave these settings unchanged for a simple personal installation.
You must set the `base_url`, or remove it for get dynamically the url from request (not recommended).

```php
return [
	'base_url' => 'https://myaswesomedomain.com', // no trailing slash
	'storage_dir' => 'storage',
	'db' => [
		'connection' => 'sqlite',
		'dsn' => 'resources/database/xbackbone.db',
		'username' => null, // username and password not needed for sqlite
		'password' => null,
	]
];
```
+ Finally, run the migrate script to setup the database

```sh
php bin/migrate --install
```
+ Now just login with `admin/admin`, **be sure to change these credentials after your first login**.

#### Changing themes
XBackBone supports all [bootswatch.com](https://bootswatch.com/) themes:
+ Run the command `php bin/theme` to see the available themes.
+ Use the same command with the argument name (`php bin/theme <THEME-NAME>`) to choose a theme.
+ If you want to revert back to the original bootstrap theme, run the command `php bin/theme default`.

#### Docker deployment
+ [Docker container](https://hub.docker.com/r/pe46dro/xbackbone-docker)

## ShareX Configuration
Once you are logged in, just go in your profile settings and download the ShareX config file for your account.

## Notes
If you do not use Apache, or the Apache `.htaccess` is not enabled, set your web server so that the `static/` folder is the only one accessible from the outside, otherwise even private uploads and logs will be accessible!
The NGINX configuration should be something like this:
```
# nginx configuration

location /app {
  return 403;
}

location /bin {
  return 403;
}

location /bootstrap {
  return 403;
}

location /resources {
  return 403;
}

location /storage {
  return 403;
}

location /vendor {
  return 403;
}

location /logs {
  return 403;
}

autoindex off;

location / {
  if (!-e $request_filename){
    rewrite ^(.*)$ /index.php break;
  }
}
```

## Built with
+ FlightPHP (http://flightphp.com/)
+ Bootstrap 4 (https://getbootstrap.com/)
+ Font Awesome 5 (http://fontawesome.com)
+ ClipboardJS (https://clipboardjs.com/)
+ HighlightJS (https://highlightjs.org/)
+ JQuery (https://jquery.com/)
