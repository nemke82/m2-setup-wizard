# m2-setup-wizard
Magento 2 Extension for adding Web Setup Wizard

The idea behind this module/extension is to fix issue with missing Web Wizard button when static files are served from pub/ folder and when Nginx as a web server is used.

--Installing the Extension--

While you're free to manually install the webwizard extension (and the use of the app/code folder structure supports this), we recommend using Magento's PHP composer integration to install the extension (https://getcomposer.org/). All Magento 2 systems have a composer.json file, and this file is how developers and Magento Marketplace users get new packages in and out of their system.

Installing the extension is a X step process

Add this GitHub repository to your project as a composer repository
Add the Neman/webwizard composer package to your project
Update your project's composer dependencies
Install the downloaded package via Magento's standard command line tool

--Quick Start--

After backing up your composer.json file

cp composer.json composer.json.bak

Run
composer config repositories.neman vcs https://github.com/nemke82/m2-setup-wizard <BR>
composer require neman/webwizard --no-update <BR>
composer update neman/webwizard <BR>
php bin/magento module:enable Neman_webwizard <BR>
php bin/magento setup:upgrade <BR>

After running the above, the Neman/Webwizard extension will be installed, ready for configuration.

--Composer Details--

The first composer command
composer config repositories.foo vcs https://github.com/nemke82/m2-setup-wizard <BR>

Add this GitHub repository as a composer repository to your composer.json file:
#File: composer.json
```
"repositories": {
    "neman": {
        "type": "vcs",
        "url": "https://github.com/nemke82/m2-setup-wizard"
    }
},
"require": {
    //...
    "neman/webwizard": "^1.0"
},
```

This tells composer it should look for additional packages in this GitHub repository.

The second command: <BR>
composer require neman/webwizard --no-update <BR>
add the latest stable version of ometria/magento2 to your composer.json file's require section.

The third command:<BR>
composer update neman/webwizard <BR>

Updates any composer packages that match the string neman/webwizard. This is what triggers the download of the Neman/Webwizard extension source code to app/code/neman directory.

Things after module is enabled needs to be done:
1) php bin/magento setup:upgrade
2) php bin/magento cache:clean
3) php bin/magento cache:flush
4) rm -rf var/di/* var/generation/* var/cache/* var/log/* var/page_cache/*
5) php bin/magento setup:static-content:deploy

NOTE: YOU NEED TO SYMLINK setup/ and update/ folder from folder where your script is settled to pub/ folder, you can follow my example here with full paths: <BR>
ln -s /home/nemanja/public_html/setup /home/nemanja/public_html/pub/ <BR>
ln -s /home/nemanja/public_html/update /home/nemanja/public_html/pub/ <BR>

** Adjust paths with the real one used **

Important: Changing a Magento system running in production is not a recommended practice. Depending on your system software, or other running extensions, running setup:upgrade may trigger undesired behaviors. As will installing any new software on your system, don't forget to take appropriate backup steps, and to test your new module in a development or staging enviornment before deploying to production.

