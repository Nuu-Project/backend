# 使用官方 PHP 映像檔作為基礎映像檔
FROM php:8.2-fpm

# 安裝系統依賴
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo pdo_mysql

# 安裝 Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 設定工作目錄
WORKDIR /var/www

# 複製專案檔案
COPY . .

# 安裝 PHP 依賴
RUN composer install

# 暴露應用程式埠號
EXPOSE 9000

# 定義容器啟動時執行的命令
CMD ["php-fpm"]
