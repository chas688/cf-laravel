# Cloud Foundry + Laravel 5.5
I recently had to set up a Cloud Foundry based Laravel app and found a surprising lack of information out there on it. Most of what is out there is
outdated PHP <7.0. 

This uses the Cloud Foundry PHP build pack: https://github.com/cloudfoundry/php-buildpack and PHP7.0

You'll need to modify the manifest.yml and add your own [app_name] to launch it.
Additionally, you can set the APP_DEBUG=true in the manifest as well to debug
any Laravel issues.

One interesting thing and I think it's a bug in CF is that the 
storage/framework/* empty directories don't push up, unless there is something
in them, thus the added .txt empty files in there to allow this to happen.

the http/ directory contains all the laravel source code, but the trick with the buildpack
is to add the composer.json and composer.lock file to the root of the project. This has been done, but the 
composer.json has been modified to reflect the htdocs/ directory. Otherwise, any composer 
post-install artisan commands will not run.

## Install and Run
 
1. install the CF cli tools:
http://docs.cloudfoundry.org/cf-cli/
2. Check out this code <code>git clone https://github.com/chas688/cf-laravel.git</code>
3. <code>cd cf-laravel</code>
4. Change the name from [app_name] to your app name in manifest.yml
5. <code>cf push</code>

