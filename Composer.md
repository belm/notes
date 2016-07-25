# Composer

## Install

*全局安装  [下载](https://getcomposer.org/installer)*

```
mv composer.phar /usr/local/bin/composer
composer 或者  php composer.phar 
```

*Homebrew安装*

```
brew tap josegonzalez/homebrew-php  
brew install josegonzalez/php/composer
```

## [Usage](https://getcomposer.org/doc/01-basic-usage.md)

*创建`composer.json`文件*

```
{
	"require": {
		"monolog/monolog": "1.0.*" 
	}
}
```
*Installing Dependencies*

```
composer install  //will created a composer.lock file
```

*composer.lock - The Lock File*

1. install命令检测到composer.lock文件存在，就会直接使用此配置，忽略json的配置。
2. 不存在composer.lock文件,执行install或update会从json里面读取依赖和版本号，生成lock文件
3. 依赖更新时，不会自动更新，执行udpate，会从json读取最新配置，更新lock文件

```
composer update //更新所有
composer update monolog/monolog [...] //更新指定的依赖
composer update nothing //增加了描述，不打算更新任何库,仅仅为了同步lock
或者
composer update --lock //新版本支持
```
## 更新composer
```
composer self-update
```

## 不编辑composer.json的情况下安装库
```
composer require "foo/bar:1.0.0" //安装新依赖库
composer init --require=foo/bar:1.0.0 -n --profile//自己创建json文件,使用-n,不用回答问题,--profile显示执行时间
```

## 考虑缓存，dist包优先;若要修改，源代码优先

dist包也可以用于诸如dev-master之类的分支，Github允许你下载某个git引用的压缩包。为了强制使用压缩包，而不是克隆源代码，你可以使用install和update的--prefer-dist选项，可以使用--prefer-source来强制选择克隆源代码.

```
composer update symfony/yaml --prefer-source  
```

## 生产环境优化自动加载
```
composer dump-autoload --optimize  
```
>安装包的时候可以同样使用--optimize-autoloader。不加这一选项，你可能会发现20%到25%的性能损失。


##Packagist / Composer 中国全量镜像
### 镜像地址
[官方地址](https://packagist.org/) [中国地址](http://pkg.phpcomposer.com/)
镜像地址：<https://packagist.phpcomposer.com>
### 用法
- 系统全局配置： 即将配置信息添加到 Composer 的全局配置文件 config.json 中
- 单个项目配置： 将配置信息添加到某个项目的 composer.json 文件中

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com //全局配置

composer config repo.packagist composer https://packagist.phpcomposer.com //进行项目根目录，单个项目配置
```


