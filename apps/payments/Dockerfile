FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd sockets
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /app
COPY . .
RUN touch ./database/database.sqlite
RUN composer install
RUN cp .env.example .env
RUN php artisan key:generate
RUN php artisan migrate:fresh
CMD sleep 15 && php artisan rabbitmq:consume
