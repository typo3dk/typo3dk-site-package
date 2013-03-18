TYPO3 Danmark
=============

TYPO3 Danmark Neos site package

Installation instructions
-------------------------

This package can either be installed in a neos basis distribution, or used via te typo3dk-base-distribution which
already has a requirement on this site package.

Please make sure you have composer installed on you system. See [http://getcomposer.org/](http://getcomposer.org/) for
installation instructions.

To do a fresh install from a neos-base-distribution, follow these steps.

    composer create-project -s dev  typo3/neos-base-distribution flow

Set your webserver to point to the flow/Web folder

Then create a new database and edit flow/Configuration/Settings.yaml to reflect your settings

Example:

```yaml
TYPO3:
  Flow:
    persistence:
      backendOptions:
        host: '127.0.0.1'
        dbname: 'typo3dk_neos'
        user: 'typo3dk_neos'
        password: ''
  Neos:
    loadMinifiedJavascript: FALSE
```

Then make sure you update your database with required tables and fields.

    cd flow
    ./flow doctrine:create

Next use composer to fetch the latest typo3dk site package

    composer require typo3dk/typo3dk

When asked for version, type dev-master

And then import the typo3.dk site into you installation.

    ./flow site:import --package-key TYPO3DK.typo3dk

Last, create a new admin user for editing the site

    ./flow user:create --username USERNAME --password YOURPASSWORD --first-name YOURFIRSTNAME--last-name YOURLASTNAME --roles "Administrator"

Depending on your file permissions and user-setup, you might need to reset all permissions with (Adjust www-data to the user that runs you apache webserver)

    ./flow flow:core:setfilepermissions www-data www-data www-data

Enjoy!

