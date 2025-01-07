# Imagem base do Apache com PHP
FROM php:7.4-apache

# Instalar dependências necessárias
RUN apt-get update && apt-get install -y \
    phpmyadmin \
    libapache2-mod-php \
    && apt-get clean

# Habilitar o módulo do Apache para PHP
RUN a2enmod php7.4

# Configuração do PHPMyAdmin
RUN ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

# Copiar arquivos de configuração
COPY ./conf/ /tmp/conf/

# Definir variáveis de ambiente para o OCS Inventory
ENV OCS_DB_SERVER=db_server
ENV OCS_DB_PORT=3306
ENV OCS_DB_NAME=ocsinventory
ENV OCS_DB_USER=root
ENV OCS_DB_PASS=password

# Instalar o OCS Inventory e configurar o ambiente
RUN mkdir -p /var/www/html/ocsreports \
    && mkdir -p /var/lib/ocsinventory \
    && chown -R www-data:www-data /var/www/html /var/lib/ocsinventory

# Expor a porta 80 para o Apache
EXPOSE 80

# Iniciar o Apache
CMD ["apache2-foreground"]
