# Laravel

## gitlab 创建项目

## clone gitlab 项目到本地

## 安装 laravel 项目

```bash
composer create-project --prefer-dist laravel/laravel blog
```

## 修改 timezone

```php
'timezone' => 'PRC'
```

## 安装 telescope

```bash
composer require laravel/telescope
php artisan telescope:install
php artisan migrate
php artisan telescope:publish
```

### 修改 telescope 虚拟目录

copy from vendor and paste to: resources/views/vendor/telescope/layout.blade.php

- Original:

    ```html
    <!-- Global Telescope Object -->
    <script>
        window.Telescope = @json($telescopeScriptVariables);
    </script>
    ```

- Updated:

    ```html
    <!-- Global Telescope Object -->
    <script>
        window.Telescope = @json($telescopeScriptVariables);

        var telescopePath = "{{ ltrim(parse_url(url(config('telescope.path')))['path'], '/') }}";
        window.Telescope.path = telescopePath;
    </script>
    ```

### sqlite 文件压缩

```bash
sqlite3 /srv/www/service/database/telescope.sqlite "vacuum;"
```
