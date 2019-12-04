# offline-nginx
A sample website to return a 503 for all queries when your website is offline

I copy this entire directory to /usr/local/www/offline

In my nginx.conf file I have:

    include /usr/local/etc/nginx/includes/*.conf;

In that directory, I have this:

```
$ ls -l /usr/local/etc/nginx/includes
total 6
lrwxr-xr-x  1 root  wheel    54 Oct 14 21:29 default.conf -> /usr/local/www/default_vhost/configuration/vhosts.conf
lrwxr-xr-x  1 root  wheel    43 Nov  9  2018 freshports.org.conf.inactive -> /usr/local/etc/freshports/vhosts.conf.nginx
lrwxr-xr-x  1 root  wheel    48 Dec  4 13:18 offline.conf -> /usr/local/www/offline/configuration/vhosts.conf
```

Ignore default.conf

You can see that I use symlinks to the actual configuration file.

Since Nginx includes only `*.conf` files, I have renamed the freshports.org.

## When going offline I do this:

```
mv freshports.org.conf freshports.org.conf.inactive
mv offline.conf.inactive offline.conf
service nginx configtest
service nginx restart
```

## When going online:

```
mv freshports.org.conf.inactive freshports.org.conf
mv offline.conf offline.conf.inactive
service nginx configtest
service nginx restart
```


Hope this helps.
