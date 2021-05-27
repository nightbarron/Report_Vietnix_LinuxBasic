# PHP-FPM

<VirtualHost *:80>                                                                                                              
    ServerName test1.com                             
    DocumentRoot /var/www/test1.com/html                                                                                    
    ErrorLog /home/logs/httpd/error_test1.com                                                                               
    CustomLog /home/logs/httpd/access_test1.com combined                                                                                                                                                              
    ProxyPassMatch ^/(.*\.php)$ fcgi://127.0.0.1:9074/var/www/test1.com/html/$1

    <Directory /var/www/test1.com/html>                                                                                             
        AllowOverride All                                                                                                       
        Require all granted                                                                                             
    </Directory>    

</VirtualHost>



# PHP_CGI

<VirtualHost *:80>
    ServerAdmin webad01@localhost
    DocumentRoot /home/webad01/public_html
    ServerName webad01.info
    
    AddHandler vietnix-php .php
    Action vietnix-php /vietnix-cgi/php56.cgi
    ScriptAlias /vietnix-cgi/ /home/webad01/vietnix-cgi/

    <Directory /home/webad01/vietnix-cgi/>
        # Options +ExecCGI    
	    Require all granted
    </Directory>

    <Directory /home/webad01/public_html>
            Options +Indexes +FollowSymLinks +ExecCGI
            AllowOverride All
            DirectoryIndex index.php
            Require all granted
    </Directory>
</VirtualHost>

# Nginx Reverse Proxy (serve static files)

server {
        listen 80;
        server_name webad02.info; #change to your domain name
        root    /home/webad02/public_html;

        error_log       /home/logs/nginx/error_nginx;

        location / {
                try_files $uri @proxy ;
        }

        location @proxy {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
                proxy_pass http://127.0.0.1:8080;  #change to your internal server IP
                proxy_redirect off;
        }


}

# Default Nginx for Wordpress

# Upstream to abstract backend connection(s) for php
upstream php {
        server unix:/tmp/php-cgi.socket;
        server 127.0.0.1:9000;
}

server {
        ## Your website name goes here.
        server_name domain.tld;
        ## Your only path reference.
        root /var/www/wordpress;
        ## This should be in your http block and if it is, it's not needed here.
        index index.php;

        location = /favicon.ico {
                log_not_found off;
                access_log off;
        }

        location = /robots.txt {
                allow all;
                log_not_found off;
                access_log off;
        }

        location / {
                # This is cool because no php is touched for static content.
                # include the "?$args" part so non-default permalinks doesn't break when using query string
                try_files $uri $uri/ /index.php?$args;
        }

        location ~ \.php$ {
                #NOTE: You should have "cgi.fix_pathinfo = 0;" in php.ini
                include fastcgi_params;
                fastcgi_intercept_errors on;
                fastcgi_pass php;
                #The following parameter can be also included in fastcgi_params file
                fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
                expires max;
                log_not_found off;
        }
}



