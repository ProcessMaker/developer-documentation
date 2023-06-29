---
description: >-
  The Skeleton Package is a template to get started with ProcessMaker Platform
  Packages
---

# The Package Skeleton

## Getting Started

This package provides the necessary base to start developing a package for ProcessMaker Platform.

Since ProcessMaker Platform is built upon the Laravel framework, this is essentially a skeleton package for Laravel, with a few ProcessMaker additions for ease of development.

If you want to dive deeper into package capabilities, please visit the [laravel documentation site](https://laravel.com/docs).

## Clone the repo

`git clone https://github.com/Processmaker/package-skeleton.git &&` cd package-skeleton

`php rename-project.php package-skeleton`

`composer update && composer install`

`npm install && npm run dev`

## Installation

* Use `composer require processmaker/package-skeleton` to install the package.
* Use `php artisan package-skeleton:install` to install generate the dependencies.

## Navigation and testing

* Navigate to the admin menu in your ProcessMaker Platform instance.
* Select `Skeleton Package` from the administrative sidebar.

## Uninstall

* Use `php artisan package-skeleton:uninstall` to uninstall the package.
* Use `composer remove processmaker/package-skeleton` to remove the package completely.

