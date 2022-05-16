# Setup

Create a new directory for the error page to life
```bash
sudo mkdir -p /var/www/maintenance && cd /var/www/maintenance
```

Download the error page and unzip it
```bash
sudo wget https://gitlab.com/Dafnik/meta/-/archive/main/meta-main.zip?path=maintenance && unzip ./meta-main.zip?path=maintenance && rm 'meta-main.zip?path=maintenance'
```

Lastly, move everything into place
```bash
mv meta-main-maintenance/maintenance/* ./ && rm -r meta-main-maintenance/
```

## Nginx
### Configuration via a snippet

Create a new file under `/etc/nginx/snippets/berror.conf`
```bash
sudo mkdir -p /etc/nginx/snippets/ && nano berror.conf
```

And paste the following content into it
```bash
error_page 404 403 500 502 503 /error.html;
location = /error.html {
        root /var/www/maintenance;
        internal;
}
```

You can customize different errors which should be catched.

Last but not least include the snippet in your site server block
```bash
include snippets/berror.conf;
```

### Configuration in site config
Add the following lines in your `server` block
```bash
error_page 404 403 500 502 503 /error.html;
location = /error.html {
        root /var/www/maintenance;
        internal;
}
```
