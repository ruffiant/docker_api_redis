FROM php:8.2-fpm

# 安装系统依赖
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    librabbitmq-dev \
    libssh-dev \
    libzip-dev

# 清理apt缓存
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# 安装PHP扩展
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# 安装Redis扩展
RUN pecl install redis && docker-php-ext-enable redis

# 安装AMQP扩展
RUN pecl install amqp && docker-php-ext-enable amqp

# 安装Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 设置工作目录
WORKDIR /var/www/html

# 配置PHP
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# 暴露端口
EXPOSE 9000

CMD ["php-fpm"]