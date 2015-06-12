# Requirements

To run GotCms, your system needs to have:

* [PHP](http://www.php.net/): **version 5.3** or greater
* [MySQL](http://www.mysql.com/) **version 5.x** or greater or [PostgreSQL](http://www.postgresql.org/) **version 8.4** or greater
* Native **PDO** support
* A web server that supports PHP like Apache, Nginx or cherokee.

## About the web server and clean urls

During development of GotCms and in creating our documentation, we always assume you’ll be running the Apache web server. However, this does not mean GotCms only runs on Apache.

In prinicple any web server that supports PHP can be used.

In the case of Apache, the rewrite rules and other options in the .htaccess file will only work, if you have at least the following in your VirtualHost’s configuration file:

```
<VirtualHost *:80>
    ServerAdmin admin@got-cms.com
    ServerName got-cms.com
    ServerAlias www.got-cms.com
    DocumentRoot /var/www/got-cms/public
    <Directory /var/www/got-cms/public>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride None
        Order allow,deny
        RewriteEngine On
        RewriteCond %{REQUEST_FILENAME} -s [OR]
        RewriteCond %{REQUEST_FILENAME} -l [OR]
        RewriteCond %{REQUEST_FILENAME} -d
        RewriteRule ^.*$ - [NC,L]
        RewriteRule ^.*$ index.php [NC,L]
    </Directory>
</VirtualHost>
```

## GotCms is known to work with

* MySQL ([http://www.mysql.com/](http://www.mysql.com/))
* PostgreSQL ([http://www.postgresql.org/](http://www.postgresql.org/))
* Apache ([http://www.apache.org/](http://www.apache.org/))
