---
layout: post
title: "Laravel 从零开始入门-laradock"
description: "Docker环境"
category: 技术
tags: [Laravel]
---

[TOC]

---

# 搭建环境

## 安装Docker

请查阅官方文档
![](/assets/images/15180867691292.jpg)



##  切换国内源

推荐使用Docker官方国内源`https://registry.docker-cn.com`

![](/assets/images/15180867819782.jpg)



## 使用`laradock`

参考教程：http://laravelacademy.org/post/7691.html

```
git clone https://github.com/Laradock/laradock.git
```

## 安装`composer`以及`laravel`命令

参考官网：

```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

# 建议把文件移动至/usr/local/bin/composer
sudo mv composer.phar /usr/local/bin/composer
```

配置国内镜像源，建议全局配置：

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

安装`laravel`命令：

```
composer global require "laravel/installer"
# 安装好之后路径在这
~/.composer/vendor/bin/laravel
```

## 新建一个 `blog`

```
mkdir ../wwwroot
cd ../wwwroot
~/.composer/vendor/bin/laravel new blog
cd blog
cp env-example .env
```

##  回到`laradock`目录继续进行一些配置


---

我的快速配置

# 关于`blog`的`.env`的配置

```
DB_CONNECTION=mysql
DB_HOST=laradock_mysql_1
DB_PORT=3306
DB_DATABASE=user_test
DB_USERNAME=root
DB_PASSWORD=root
```

这里配置了 mysql的服务器为`laradock_mysql_1`，端口是`3306`，数据库使用`user_test`，用户名、密码等。

# 关于数据库的配置

使用phpmyadmin查看到的效果如下：

这个数据库`user_test`有一张表，名字是`user_name`，有4个字段，分别是`id`, `name`, `email`和`address`。

这个phpmyadmin启动的命令是：
![](/assets/images/15180868032532.jpg)


```
docker run --name myadmin --net laradock_backend -d --link laradock_mysql_1:db -p 8080:80 phpmyadmin/phpmyadmin
```
如何知道这个`laradock_mysql_1`的docker网络环境？使用`docker network ls`查看即可。

![](/assets/images/15180868275209.jpg)

# 代码编写过程

```
php artisan make:model  Model\user # → app/Model/user.php
php artisan make:controller UserController # → app/Http/Controllers/UserController.php
```

## `app/Model/user.php`文件

```php
class user extends Model
{
    //generated by php artisan make:model Model\user
    protected $table = 'user_name';
    protected $primaryKey = 'id';
    protected $guarded = [];
    public $timestamps = false;
}
```

## `app/Http/Controllers/UserController.php`文件

```php
class UserController extends Controller
{
    // generate by php artisan make:controller UserController
    public function action_index()
    {
        echo "饭局狼人杀：我是猎人我怕谁？";
        $data = user::all();
        dd($data);
    }
}
```

## 路由配置`routes/web.php`
```php
Route::get('/user', 'UserController@action_index');
```

我的入门学习链接：
1，http://blog.csdn.net/mzjmc123/article/details/75405852
2，http://laravelacademy.org/post/7691.html








