# Configuração do Nginx no Linux Mint

Este é um guia passo a passo para configurar o servidor Nginx no Linux Mint OS.

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

