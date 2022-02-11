FROM php:8.0.9-fpm

WORKDIR /app
RUN docker-php-ext-install pcntl

COPY /src .

EXPOSE 8080

CMD ["php", "artisan", "octane:start", "--host", "0.0.0.0", "--port", "8080"]

