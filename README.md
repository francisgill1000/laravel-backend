1@Ab56ab56

sudo apt update && sudo apt upgrade -y

sudo apt install php-cli php-mbstring php-xml composer php-curl php-zip php-bcmath php-tokenizer sqlite3 php-sqlite3 nginx -y

cd /etc/nginx/sites-available

sudo nano laravel

server {
listen 8000;
server_name localhost;

    root /var/www/backend/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

}

sudo ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/

sudo service nginx reload
