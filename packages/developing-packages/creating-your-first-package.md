---
description: >-
  Learn how to develop a custom package for ProcessMaker Platform to extend its
  functionality.
---

# Creating Your First Package

## Overview

Extend ProcessMaker's functionality with custom functions and/or integrations with third-party services by developing your own [package](broken-reference).

## Requirements

The following are required or assumed to successfully create a package for ProcessMaker Platform:

* You are a developer that is comfortable performing command-line operations. This is an advanced development topic.
* You are comfortable and knowledgeable about [Laravel artisan commands](https://laravel.com/docs/8.x/packages). See [Laravel documentation](https://laravel.com/docs/8.x).
* ProcessMaker Platform is installed on your local computer.
* PHP version 7 or later.

## Create a Package

Follow these steps to create a package for ProcessMaker Platform:

1.  Create a directory as a sibling directory to your local ProcessMaker Platform installation directory. This example names the new directory `processmaker-plugins`.

    For example, if your ProcessMaker Platform installation is within the directory `opt/processmaker`, create the `processmaker-plugins` directory at `Documents/processmaker-plugins`.

    `mkdir processmaker-plugins`
2.  Clone the [`package-skeleton`](https://github.com/ProcessMaker/package-skeleton) GitHub repository into your `processmaker-plugins` directory.

    `cd processmaker-plugins`

    `git clone https://github.com/ProcessMaker/package-skeleton`
3.  Rename the cloned directory. This example uses the new name `my-first-package`.

    `mv package-skeleton my-first-package`
4.  Change to the renamed directory, `my-first-package`.

    `cd my-first-package`
5.  Rename the references of "package-skeleton" to the revised name of your package skeleton, "my-first-package". The following command renames all instances in the project.

    `php rename-project.php my-first-package`
6.  Edit the following JSON objects in the `composer.json` file from the package:

    * **name:** Edit the `name` JSON object that references the directory path to your package development environment, such as `my-first-package`.
    * **friendly\_name:** Edit the `friendly_name` JSON object to the name of your revised project directory, such as "My First Package".

    Perform these commands:

    `cd my-first-package`

    `vim composer.json`

    Below is an example of these JSON objects in the `composer.json` file in the `my-first-package` directory after they are edited:

    ```json
    {
        "name": "processmaker/my-first-package",
        "friendlY_name": "My First Package",
        "description": "Package Skeleton to develop a package for ProcessMaker Platform"
    } 
    ```
7. Save the changes: press the **Esc** key and enter `:wq` to save the `composer.json` file and exit from vim.
8.  In your local ProcessMaker Platform installation, locate the `composer.json` file, and add a reference to your package in the `repositories` JSON array.

    `cd /opt/processmaker`

    `vim composer.json`

    Below is an example of the `repositories` JSON array in the `composer.json` file in the `my-first-package` directory after they are edited:&#x20;

    ```json
    "repositories": [
    {
        "type": "path",
        "url": "../processmaker-plugins/my-first-package",
    }]
    ```
9. Save the changes: press the **Esc** key and enter `:wq` to save the `composer.json` file and exit from vim.
10. Edit the `console.php` file located inside your package to set up that package with the artisan commands in line 3 of that file. The commands below reference the `processmaker-plugins/my-first-package` directory since this example names the package as such:

    `cd /opt/`

    `cd processmaker-plugins/my-first-package`

    `cd routes`

    `vim console.php`
11. Save the changes: press the **Esc** key and enter `:wq` to save the `composer.json` file and exit from vim.
12. Build your package repository assets inside your package. The second command below references the `processmaker-plugins/my-first-package` directory since this example names the package as such:

    `cd /opt/`

    `cd processmaker-plugins/my-first-package/`

    `npm install`

    `npm run development`
13. Rename the controller file `PackageSkeletonController.php` to the name of your package's name. Since this package uses the name `processmaker-plugins/my-first-package`, this example changes `PackageSkeletonController.php` to `MyFirstPackageController.php`:

    `cd processmaker-plugins/my-first-package`

    `cd src/Http/Controllers`

    `ls`
14. Inside your package, locate the controller file.

    `mv PackageSkeletonController.php MyFirstPackageController.php`
15. Open your renamed file and ensure the controller file `MyFirstPackageController.php` has the same class name as your package project's name. Since in this example uses `MyFirstPackageController.php` as renamed in the previous step, this example uses the following in line 12: `class MyFirstPackageController extends Controller`

    ```php
    class MyFirstPackageController{
        public function index(){
            return view('my-first-package::index');
        }
    }
    ```
16. Exit the file: press the **Esc** key and enter `:q`.
17. Optionally, to delete your package when uninstalling it, include the code below in the `console.php` file of your package located in the file `/opt/processmaker-plugins/my-first-package/routes/console.php`. Since this package uses the name `my-first-package` for this example, the second and fourth commands below references this name:

    `// Uninstall package-skeleton`

    `Artisan::command('my-first-package:uninstall', function () {`

    `// Remove the vendor assets`

    `Illuminate\Support\Facades\File::deleteDirectory(public_path('vendor/processmaker/my-first-package'));`

    `$this->info('The package has been uninstalled');`

    `})->describe('Uninstalls package');`
18. Install the package using composer. Install the package via composer in your ProcessMaker Platform root folder. Since this package uses the name `my-first-package` for this example, the second command below references this name:

    `cd /opt/processmaker`

    `composer require processmaker/my-first-package --ignore-platform-reqs`
19. Setup the package with the `php artisan` command in your ProcessMaker Platform root folder, referencing the name of your package. Since this package uses the name `my-first-package` for this example, the command below references this name:

    `php artisan my-first-package:install`

## Uninstall the Package

Follow these steps to uninstall a custom package:

1. Go to the ProcessMaker root directory, such as `/opt/processmaker`.
2.  Run the following commands, changing `my-first-package` in the second command to the directory name of your package:

    `php artisan my-first-package:uninstall`

    `composer remove processmaker/my-first-package --ignore-platform-reqs`
