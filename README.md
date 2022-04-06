<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Yii 2 Basic Project Template</h1>
    <br>
</p>

Yii 2 Basic Project Template is a skeleton [Yii 2](http://www.yiiframework.com/) application best for
rapidly creating small projects.

The template contains the basic features including user login/logout and a contact page.
It includes all commonly used configurations that would allow you to focus on adding new
features to your application.

[![Latest Stable Version](https://img.shields.io/packagist/v/yiisoft/yii2-app-basic.svg)](https://packagist.org/packages/yiisoft/yii2-app-basic)
[![Total Downloads](https://img.shields.io/packagist/dt/yiisoft/yii2-app-basic.svg)](https://packagist.org/packages/yiisoft/yii2-app-basic)
[![build](https://github.com/yiisoft/yii2-app-basic/workflows/build/badge.svg)](https://github.com/yiisoft/yii2-app-basic/actions?query=workflow%3Abuild)

DIRECTORY STRUCTURE
-------------------

      assets/             contains assets definition
      commands/           contains console commands (controllers)
      config/             contains application configurations
      controllers/        contains Web controller classes
      mail/               contains view files for e-mails
      models/             contains model classes
      runtime/            contains files generated during runtime
      tests/              contains various tests for the basic application
      vendor/             contains dependent 3rd-party packages
      views/              contains view files for the Web application
      web/                contains the entry script and Web resources



REQUIREMENTS
------------

The minimum requirement by this project template that your Web server supports PHP 5.6.0.


INSTALLATION
------------

### Install via Composer

If you do not have [Composer](http://getcomposer.org/), you may install it by following the instructions
at [getcomposer.org](http://getcomposer.org/doc/00-intro.md#installation-nix).

You can then install this project template using the following command:

~~~
composer create-project --prefer-dist yiisoft/yii2-app-basic basic
~~~

Now you should be able to access the application through the following URL, assuming `basic` is the directory
directly under the Web root.

~~~
http://localhost/basic/web/
~~~

### Install from an Archive File

Extract the archive file downloaded from [yiiframework.com](http://www.yiiframework.com/download/) to
a directory named `basic` that is directly under the Web root.

Set cookie validation key in `config/web.php` file to some random secret string:

```php
'request' => [
    // !!! insert a secret key in the following (if it is empty) - this is required by cookie validation
    'cookieValidationKey' => '<secret random string goes here>',
],
```

You can then access the application through the following URL:

~~~
http://localhost/basic/web/
~~~


### Install with Docker

Update your vendor packages

    docker-compose run --rm php composer update --prefer-dist
    
Run the installation triggers (creating cookie validation code)

    docker-compose run --rm php composer install    
    
Start the container

    docker-compose up -d
    
You can then access the application through the following URL:

    http://127.0.0.1:8000

**NOTES:** 
- Minimum required Docker engine version `17.04` for development (see [Performance tuning for volume mounts](https://docs.docker.com/docker-for-mac/osxfs-caching/))
- The default configuration uses a host-volume in your home directory `.docker-composer` for composer caches


CONFIGURATION
-------------

### Database

Edit the file `config/db.php` with real data, for example:

```php
return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=localhost;dbname=yii2basic',
    'username' => 'root',
    'password' => '1234',
    'charset' => 'utf8',
];
```

**NOTES:**
- Yii won't create the database for you, this has to be done manually before you can access it.
- Check and edit the other files in the `config/` directory to customize your application as required.
- Refer to the README in the `tests` directory for information specific to basic application tests.


TESTING
-------

Tests are located in `tests` directory. They are developed with [Codeception PHP Testing Framework](http://codeception.com/).
By default, there are 3 test suites:

- `unit`
- `functional`
- `acceptance`

Tests can be executed by running

```
vendor/bin/codecept run
```

The command above will execute unit and functional tests. Unit tests are testing the system components, while functional
tests are for testing user interaction. Acceptance tests are disabled by default as they require additional setup since
they perform testing in real browser. 


### Running  acceptance tests

To execute acceptance tests do the following:  

1. Rename `tests/acceptance.suite.yml.example` to `tests/acceptance.suite.yml` to enable suite configuration

2. Replace `codeception/base` package in `composer.json` with `codeception/codeception` to install full-featured
   version of Codeception

3. Update dependencies with Composer 

    ```
    composer update  
    ```

4. Download [Selenium Server](http://www.seleniumhq.org/download/) and launch it:

    ```
    java -jar ~/selenium-server-standalone-x.xx.x.jar
    ```

    In case of using Selenium Server 3.0 with Firefox browser since v48 or Google Chrome since v53 you must download [GeckoDriver](https://github.com/mozilla/geckodriver/releases) or [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) and launch Selenium with it:

    ```
    # for Firefox
    java -jar -Dwebdriver.gecko.driver=~/geckodriver ~/selenium-server-standalone-3.xx.x.jar
    
    # for Google Chrome
    java -jar -Dwebdriver.chrome.driver=~/chromedriver ~/selenium-server-standalone-3.xx.x.jar
    ``` 
    
    As an alternative way you can use already configured Docker container with older versions of Selenium and Firefox:
    
    ```
    docker run --net=host selenium/standalone-firefox:2.53.0
    ```

5. (Optional) Create `yii2basic_test` database and update it by applying migrations if you have them.

   ```
   tests/bin/yii migrate
   ```

   The database configuration can be found at `config/test_db.php`.


6. Start web server:

    ```
    tests/bin/yii serve
    ```

7. Now you can run all available tests

   ```
   # run all available tests
   vendor/bin/codecept run

   # run acceptance tests
   vendor/bin/codecept run acceptance

   # run only unit and functional tests
   vendor/bin/codecept run unit,functional
   ```

### Code coverage support

By default, code coverage is disabled in `codeception.yml` configuration file, you should uncomment needed rows to be able
to collect code coverage. You can run your tests and collect coverage with the following command:

```
#collect coverage for all tests
vendor/bin/codecept run --coverage --coverage-html --coverage-xml

#collect coverage only for unit tests
vendor/bin/codecept run unit --coverage --coverage-html --coverage-xml

#collect coverage for unit and functional tests
vendor/bin/codecept run functional,unit --coverage --coverage-html --coverage-xml
```

You can see code coverage ![25](https://user-images.githubusercontent.com/55030527/161861234-3e4b7416-0afb-41a4-9b44-a01401241613.png)
![1](https://user-images.githubusercontent.com/55030527/161861237-6bbe3804-7161-47b0-9e0b-be7e9558dc68.png)
![2](https://user-images.githubusercontent.com/55030527/161861239-ad463a8a-f953-4cbe-a371-b481632bd6ff.png)
![3](https://user-images.githubusercontent.com/55030527/161861240-a6ab73fe-556e-42ab-82a4-6a36199fbaba.png)
![4](https://user-images.githubusercontent.com/55030527/161861241-948fe1f6-b062-4bae-aaa8-1d9fb237fe59.png)
![5](https://user-images.githubusercontent.com/55030527/161861242-f337a074-a604-483c-9312-29757c4a1da1.png)
![6](https://user-images.githubusercontent.com/55030527/161861245-6624ceb2-2b2c-4fda-ba47-09cc5e108010.png)
![7](https://user-images.githubusercontent.com/55030527/161861246-56ef9fdf-f42f-4cfa-9bbd-14bb052eb6db.png)
![8](https://user-images.githubusercontent.com/55030527/161861247-e2a8061d-eaf8-4416-8782-30bffc12cce1.png)
![9](https://user-images.githubusercontent.com/55030527/161861248-2f754c61-b690-4d32-a7f2-441125791679.png)
![10](https://user-images.githubusercontent.com/55030527/161861249-8cc3c084-6c2b-4649-ba88-c769fe9204ce.png)
![11](https://user-images.githubusercontent.com/55030527/161861251-1940c1da-039f-4588-82be-241ce59433f8.png)
![12](https://user-images.githubusercontent.com/55030527/161861256-1e6683e5-6340-4308-a68f-5d945b547d7c.png)
![13](https://user-images.githubusercontent.com/55030527/161861258-ce361913-ef9a-48c8-ac0c-c33cde932099.png)
![14](https://user-images.githubusercontent.com/55030527/161861260-1e32c34e-75a3-4dbb-8bbd-d8b725a49e0c.png)
![15](https://user-images.githubusercontent.com/55030527/161861261-acd9770a-fceb-41c8-b9d3-7d8e6b83ef07.png)
![16](https://user-images.githubusercontent.com/55030527/161861265-39498a12-5ec5-4158-950f-a729cd213f88.png)
![17](https://user-images.githubusercontent.com/55030527/161861266-679e8da2-2c5c-4648-9ff4-b74b6b0c4c04.png)
![18](https://user-images.githubusercontent.com/55030527/161861268-4437b227-6eea-48b1-884b-32745932a96b.png)
![19](https://user-images.githubusercontent.com/55030527/161861269-bb82faf8-8d25-4ac8-bc67-0dc653254118.png)
![20](https://user-images.githubusercontent.com/55030527/161861271-045a7b4c-1455-45aa-aaf2-3b6e6852e527.png)
![21](https://user-images.githubusercontent.com/55030527/161861272-b9d0c29b-5de4-4463-a506-4187bf31796e.png)
![22](https://user-images.githubusercontent.com/55030527/161861274-4636c332-c975-4a3b-ad2f-a052c77a0be7.png)
![23](https://user-images.githubusercontent.com/55030527/161861275-b49a2e4f-1f2b-4733-8eb7-fe2c9b89c97d.png)
![24](https://user-images.githubusercontent.com/55030527/161861277-3c0402bc-6b38-425c-ae68-d3aba5432815.png)
output under the `tests/_output` directory.
