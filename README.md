Octivi - Yealink PhoneBook Manager is no longer maintained
=============================================

Simple PHP application to manage your Yealink Remote phone book.

Check out the [post about the release](http://labs.octivi.com/yealink-phone-book-manager-released/) on our blog!

Installation
---------------------------------------------

### Using a release file (prefered way)

1. Download the latest release of YealinkPhoneBookManager
2. Unpack archive file under your web directory
3. Modify .htaccess to allow access to your phone book manager - as described in a .htaccess password protection

Fix Apache Permissions
---------------------------------------------
# setsebool -P httpd_can_network_connect on

First re-establish the SELinux context
# restorecon -Rv /var/www/html

Change the owner of the webroot
# chown -R apache:apache /var/www/html

Change the basic permissions
# chmod -R g+w /var/www/html
# chmod g+s /var/www/html

Establish the SELinux permissions
Make all files read only
# chcon -R -t httpd_sys_content_t /var/www/html/

Only allow write on uploads dir
# chcon -R -t httpd_sys_rw_content_t /var/www/html/phonebook



### Using Composer (for development)

Under your host directory clone this Git repository.

1. In project folder execute commands:

    curl -sS https://getcomposer.org/installer | php
    php composer.phar install

2. Copy `app/properties.json.dist` to `app/properties.json`
3. In `app/properties.json` you can set default path and file name of your phone book
4. Set the server's document root to the web/ folder

Configuration
---------------------------------------------

Location of the configuration file depends on the way of the installation:

* From a release file - `index.php`
* Composer - `app/properties.json`

In that files you will find configuration properties:

* `directory` - default directory of the phone book XML files
* `defaultFileName` - name of the default file, which manager will use as a primary phone book


.htaccess password protection
---------------------------------------------

It's possible to configure a .htaccess file to ensure Basic access authentication protection. All you have to do is to uncomment
last comment block in the .htaccess file, and set the right path of your .htpasswd file.

    AuthUserFile /path/to/your/directory/.htpasswd

Yealink phones still can't get access through basic auth, so to allow them to read your phone book files, you must edit line:

    Allow from 127.0.0.1

where 127.0.0.1 has to be your phone IP address.


Phonebook backup
---------------------------------------------

In the same directory as your orginal phonebook file is, the script will create backup files of your phonebook when clicking on the "Create Backup" button.


Copyright
---------------------------------------------

Copyright 2014 IMAGIN Sp. z o.o.
Octivi - www.octivi.com
