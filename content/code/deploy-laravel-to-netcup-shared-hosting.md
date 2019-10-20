---
title: "Deploy Laravel to Netcup Shared Hosting"
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

- Open a terminal and SSH into your hosting account: 
  ```ssh -p 22 hosting123456@youdomain.com```
- Create a subdirectory in httpdocs, the public stuff of your laravel app will
  go here in a second - 
  ```
  mkdir httpdocs/blog
  ```
- Unpack your laravel app (inside your root directory, so that it then has a
  folder called blog/) - 
  ```unzip blog.zip```
- From inside your unpacked app, move everything from the public directory into
  the subdirectory in httpdocs, which we created two steps earlier - 
  ```mv blog/public/* httpdocs/blog```
- Don't forget to move ```.htaccess```, which won't get moved because it's
  hidden - 
  ```
  mv blog/public/.htaccess httpdocs/blog
  ```
- Check if blog/public is completely empty: ```ls -la blog/public```
- Check if all files have been moved: ```ls -la httpdocs/blog```

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

## Other Stuff

- Installing composer:
  ```cd /blog``` (The app directory containing everything)
  ```wget https://getcomposer.org/composer.phar```
  ```php composer.phar install```
