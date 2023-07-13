# Configuração do Nginx no Linux Mint

Este é um guia passo a passo para configurar o servidor Nginx no Linux Mint OS.

`
Observação, para facilitar o uso do terminal do linux Mint OS, Copie o codigo e cole no terminal usando as teclas de atalho Ctrl + Insert do teclado.
`

# Abra o Terminal:
```
Terminal: Ctrl + Alt + T
```
___
# Instalar o Nginx no Mint 21.1.
```
sudo apt install git vim perl python2 python3 unzip ghostscript zlib1g zlib1g-dev apt-transport-https
````
___
# Instar o PHP 8.1.
```
sudo apt install nginx php8.1 php8.1-cli php8.1-common php8.1-fpm php8.1-mysql php8.1-opcache \
php8.1-readline php8.1-bcmath php8.1-curl php8.1-intl php8.1-mbstring php8.1-xml php8.1-zip \
php8.1-soap php-imagick php-json libapr1 libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap
```
___
# Habilitar o NGINX no terminal.
```
sudo systemctl daemon-reload
```
```
sudo systemctl enable nginx
```
```
sudo systemctl enable php8.1-fpm
```
```
sudo systemctl start nginx
```
```
sudo systemctl start php8.1-fpm
```
___
# Comando NGINX
## Mostra o status nginx
```
sudo systemctl status nginx
```
___
## Reinicia o nginx
```
sudo systemctl restart nginx
```
___
## Para o nginx
```
sudo systemctl stop nginx
```
___
## Inicia o nginx
```
sudo systemctl start nginx
```
___
# Comandos PHP
Mostra o status no PHP.
```
sudo systemctl status php8.1-fpm
```
___
## Reinicia O PHP
```
sudo systemctl restart php8.1-fpm
```
___
## Para o PHP
```
sudo systemctl stop php8.1-fpm
```
___
## Inicia o PHP
```
sudo systemctl start php8.1-fpm
```
___
# Caminhos para configurar nginx
Diretório de configuração do NGINX Server
```
/etc/nginx/                  
```
___
## configuração do NGINX Server
```
/etc/nginx/nginx.conf       
```
___
## Diretório padrão dos Sites Acessíveis do NGINX Server
```
/etc/nginx/sites-available/  
```
___
## Diretório de configuração do PHP 8.1
```
/etc/php/                   
```
___
## Arquivo de configuração do PHP-FPM 8.1 do NGINX Server
```
/etc/php/8.1/fpm/php.ini     
```
___
## Diretório padrão das Hospedagem de Site do NGINX Server
```
/var/www/html/              
```
___
## Diretório padrão dos Logs do NGINX Server
```
/var/log/nginx/               
````
___
# Habilitar o PHP
Cole no terminal para ir para config de default.
````
sudo nano /etc/nginx/sites-available/default
````
___
## Dentro de default subistitua esse codigo preste atenção ao começo.
```
root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html index.php;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # pass PHP scripts to FastCGI server
        #
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
                deny all;
        }
}
# Virtual Host configuration for example.com
#
# You can move that to a different file under sites-available/ and symlink that
# to sites-enabled/ to enable it.
#
server {
        listen 80;
        listen [::]:80;

        server_name example.com;

        root /var/www/simuladosatc.com;
        index index.html;

        location / {
                try_files $uri $uri/ =404;
        }
}
```
# Para sair e salvar: CTR + x  >>> Digite "S" >>> ENTER
___
# Testar se as configurações foram feitas.
```
sudo nginx -t
```
___
# Reinciar para garantir as modificações.
```
sudo systemctl restart nginx
```
___
## Comando para ver log em tempo real.
```
sudo tail -f /var/log/nginx/access.log
```
___

# Criando o acesso personalizado.
___
# 1. Editar o arquivo de configuração do NGINX:

```
sudo nano /etc/nginx/sites-available/simuladosatc.com
```
___
## 2. Colar o seguinte conteúdo no arquivo de configuração do NGINX:
```
server {
    listen 80;
    listen [::]:80;

    server_name simuladosatc.com;

    root /var/www/simuladosatc.com;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
___

## 3. Salvar e fechar o arquivo de configuração do NGINX.
Para fazer isso aperte CTR + X e digte "S" e aperte >>> ENTER<<<
___
## 4. Criar um link simbólico para o arquivo de configuração no diretório `sites-enabled`:
```
sudo ln -s /etc/nginx/sites-available/simuladosatc.com /etc/nginx/sites-enabled/
```
___

## 5. Verificar se não há erros de sintaxe no arquivo de configuração do NGINX:
```
sudo nginx -t
```
___
## 6. Reiniciar o serviço do NGINX:
```
sudo systemctl restart nginx
```
___
## 7. Editar o arquivo `/etc/hosts`:
```
sudo nano /etc/hosts
```
___
## 8. Adicionar uma linha ao arquivo `/etc/hosts` com o endereço IP e o nome de domínio:
```
<IP_ADDRESS> simuladosatc.com
```
___
## (Substitua `<IP_ADDRESS>` pelo endereço IP do seu servidor)
## Para saber seu ip digite 
```
ip addr show
```
___
## 9. Salvar e fechar o arquivo `/etc/hosts`.

# Para sair e salvar: CTR + x  >>> Digite "S" >>> ENTER
___
## 10. Caso de erro ao enviar arquivo faça os seguintes comandos.
```
sudo nano /etc/nginx/nginx.conf
```
___
## Dentro de http{ 
```
client_max_body_size 100;
```
___
## Depois 
```
service nginx reload 
```
___
## Alem disso para permitir o usuario enviar foto use o comando 
### !!!ATENÇÃO!!!, não é recomenado a permissão 777 por questões de segurança mas para este caso foi utilizado.
```
sudo chmod -R 777 /var/www/simuladosatc.com/uploads
```
> Daniel Freitas
