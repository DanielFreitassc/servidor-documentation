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

# Vamos configurar o servidor
primeiramente vamos desativar a configuração padrão do servidor botando um # no começo de todo o codigo repita isso em todos os locais onde tem o default.
````
sudo nano /etc/nginx/sites-available/default
````
___
# Depois disso podemos iniciar.
___
Use o comando abaixo para ir até a configuração do seu site.
````
sudo nano /etc/nginx/sites-available/meusite.com
````
___
Cole isso dentro da configuração do servidor.
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
        # Configurações para uploads de arquivos
        client_max_body_size 100M;
        fastcgi_buffers 8 16k;
        fastcgi_buffer_size 32k;
        fastcgi_param PHP_VALUE "upload_max_filesize=100M \n post_max_size=100M";

}



location /uploads {
    alias /var/www/simuladosatc.com/uploads/;
    autoindex on;
    allow all;

}

    location ~ /\.ht {
        deny all;
    }
}

```
___
# Para sair e salvar: CTR + x  >>> Digite "S" >>> ENTER
___

# Testar se as configurações foram feitas.
```
sudo nginx -t
```
___
# Agora vamos habilitar o site. 
```
sudo ln -s /etc/nginx/sites-available/meusite.com /etc/nginx/sites-enabled/
```
___
# Reinciar para garantir as modificações.
```
sudo systemctl restart nginx
```
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

## Alem disso para permitir o usuario enviar foto use o comando 
### !!!ATENÇÃO!!!, não é recomenado a permissão 777 por questões de segurança mas para este caso foi utilizado.
```
sudo chmod -R 777 /var/www/simuladosatc.com/uploads
```
```
sudo chmod -R 777 /var/www/simuladosatc.com/
```
# TESTE 
```
sudo chown -R www-data:www-data /var/www/simuladosatc.com/uploads
sudo chown -R www-data:www-data /var/www/simuladosatc.com
sudo chmod -R 755 /var/www/simuladosatc.com/uploads
sudo chmod -R 755 /var/www/simuladosatc.com
```
> Daniel Freitas
