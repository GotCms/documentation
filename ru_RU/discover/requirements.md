# Требования к хостингу

Для запуска **GotCms**, ваша система должна иметь:

* [PHP](http://www.php.net/): **версии 5.3** или выше
* [MySQL](http://www.mysql.com/) **версии 5.x** или выше или [PostgreSQL](http://www.postgresql.org/) **версии 8.4** или выше
* Поддержку **PDO**
* Веб-сервер с поддержкой PHP, такой как Apache, Nginx или Cherokee.

## О веб сервере

В процессе разработки **GotCms** и создания документации, мы все время полагали что вы будете использовать веб-сервер Apache. Однако это не значит, что **GotCms** может работать только на нем. В принципе любой веб-сервер, поддерживающий PHP может быть использовать с одинаковым успехом.

В случае с веб-сервером Apache, на нем должен быть установлен mod_rewrite и для должны быть заданы соответствующие опции и правила в .htaccess. Файл конфигурации виртуального хоста для веб-сервера Apache может иметь следующее содержание:

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

## Проверено что GotCms работает с:

* MySQL ([http://www.mysql.com/](http://www.mysql.com/))
* PostgreSQL ([http://www.postgresql.org/](http://www.postgresql.org/))
* Apache ([http://www.apache.org/](http://www.apache.org/))
