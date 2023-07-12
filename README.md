# Configuração do Nginx no Linux Mint

Este é um guia passo a passo para configurar o servidor Nginx no Linux Mint OS.

`
Observação, para facilitar o uso do terminal do linux Mint OS, Copie o codigo e cole no terminal usando as teclas de atalho Ctrl + Insert do teclado.
`

## Passo 1: Instalação do Nginx

Certifique-se de ter o Nginx instalado no seu sistema Linux Mint. Se ainda não estiver instalado, execute o seguinte comando no terminal:

```
sudo apt update
```
```
sudo apt install nginx
```
## Passo 2: Configuração das regras do firewall

Para permitir o tráfego HTTP (porta 80) e HTTPS (porta 443) para o Nginx, abra o terminal e execute os seguintes comandos:
```
sudo ufw allow 'Nginx HTTP'
```
```
sudo ufw allow 'Nginx HTTPS'
```
Certifique-se de reiniciar o serviço do Nginx para aplicar as alterações:
```
sudo service nginx restart
```
## Passo 3: Verificando o endereço IP do servidor

Para descobrir o endereço IP do seu servidor Linux Mint, execute o seguinte comando no terminal:
```
ip addr show
```
Anote o endereço IP exibido na interface de rede relevante.

## Passo 4: Testando a configuração do Nginx

Abra um navegador e digite o endereço IP do seu servidor Linux Mint na barra de endereços. Se tudo estiver configurado corretamente, você deve ver a página padrão do Nginx.

### Comandos Manutenção do serviço
Iniciar Serviço
```
sudo systemctl start nginx
```
Parar Serviço
```
sudo systemctl stop nginx 
```
Reiniciar Serviço
```
sudo systemctl restart nginx
```
Recarregar Serviço
```
sudo systemctl reload nginx
```
Desabilitar serviço
```
sudo systemctl disable nginx
```
Habilitar Serviço
```
sudo systemctl enable nginx      
```
### Para acessar a pasta onde está rodando o serviço digite via terminal
```
cd /var/www
```
```
ls
```
```
cd html
```
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
