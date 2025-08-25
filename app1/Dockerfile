# Usa uma imagem com Apache + PHP
FROM php:8.2-apache

# Porta usada pelo Render
ENV PORT=8080

# Permite URLs amigáveis
RUN a2enmod rewrite

# Copia arquivos para o diretório raiz do Apache
COPY . /var/www/html/

# Corrige permissões
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Corrige configuração da porta
RUN sed -i "s/Listen 80/Listen ${PORT}/" /etc/apache2/ports.conf && \
    sed -1 "s/<VirtualHost \*:80>/<VirtualHost *:${PORT}>/" /etc/apache2/sites-enabled/000-default.conf &&

# Permite acesso ao diretório
RUN echo '<Directory /var/www/html>' >> /etc/apache2/apache2.conf && \
    echo '    Option Indexes FollowSymLinks' >> /etc/apache2/apache2.conf && \
    echo '    AllowOverride All' >> /etc/apache2/apache2.conf && \
    echo '    Require all granted' >> /etc/apache2/apache2.conf && \
    echo '<Directory>' >> /etc/apache2/apache2.conf

# Expõe a porta corretamente
EXPOSE ${PORT}

# Inicia o Apache
CMD ["apache2-foreground"]
