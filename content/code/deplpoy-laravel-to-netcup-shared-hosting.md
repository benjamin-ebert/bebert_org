---
title: "Deplpoy Laravel to Netcup Shared Hosting"
date: 2019-10-19T10:12:49+02:00
draft: false
tags: ["Hosting"] 
---

- Login to Netcup Customer Control Panel
- Click 'Produkte'
- Click the hosting account you want to deploy your app to
- Click 'Auto-Login WEB'

- Click 'PHP-Einstellungen'
- Check 'PHP-Unterstützung' and select PHP-Version 7.3
- Under 'Allgemeine Einstellungen' > 'open_basedir', select the second option
  (the one starting with *{WEBSPACEROOT}*)
- Set *display_errors* and *log_errors* to *on* (Restore to default when you're
  done!)
- Click *Übernehmen*, your changes may take a few minutes to be applied

- On your local machine, compress the folder containing your laravel app to .zip
- Eg. compressing the folder blog/ containing app/, bootstrap/, config/ ... to
  blog.zip
- Upload blog.zip to your base directory via FTP - not into *httpdocs*
- Your root directory now looks like this: .cache/ ... bin/ ... var/ ...
  blog.zip

- Open a terminal and SSH into your hosting account: ```ssh -p 22 hosting123456@youdomain.com```
- ```mkdir httpdocs/blog```
- ```unzip blog.zip```
- ```mv blog/public/* httpdocs/blog```

- In your browser, open yourdomain.com/blog
- You should see a couple error messages about vendor/autoload.php not being
  found
- ```vi httpdocs/blog/index.php```
- Edit line 24 (may have changed by now), so that it looks like this:
  ```require __DIR__.'/../../blog/vendor/autoload.php';```
- Save index.php
- Refresh yourdomain.com/blog
- You should see a similar error message, this time mentioning bootstrap/app.php
- ```vi httpdocs/blog/index.php```
- Edit line 38 (may have changed by now), so that it looks like this: ```$app =
  require_once __DIR__.'/../../whsa/bootstrap/app.php';```

- Refresh yourdomain.com/blog
- You should see a laravel error message, typically stating some SQL error,
  because we haven't configured your database yet

## Database

- Click *Datenbanken*
- Click *Datenbank hinzufügen*
- Create databasename, username and password
- Click *Abbild importieren*
- Upload your .sql dump
- Click *Überprüfen und reparieren*
- Click *Verbindungsdaten* to view relevant settings

- Copy those settings into /blog/.env
- Dont't forget to put the DB_HOST and DB_PORT on different lines, not in one
  line, as the information form netcup suggests
- PUT THE GODDAMN PASSWORD IN SINGLEQUOTES

## Routes

- Make sure there is a .htaccess file in httpdocs/blog, and it says:
```
<IfModule mod_rewrite.c>
    <IfModule mod_negotiation.c>
        Options -MultiViews -Indexes
    </IfModule>

    RewriteEngine On

    # Handle Authorization Header
    RewriteCond %{HTTP:Authorization} .
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

    # Redirect Trailing Slashes If Not A Folder...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_URI} (.+)/$
    RewriteRule ^ %1 [L,R=301]

    # Handle Front Controller...
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [L]
</IfModule>
```
(This is the default laravel .htaccess file, normally automatically created in
blog/public)

## Other Stuff

- Installing composer:
  ```cd /blog``` (The app directory containing everything)
  ```wget https://getcomposer.org/composer.phar```
  ```php composer.phar install```
