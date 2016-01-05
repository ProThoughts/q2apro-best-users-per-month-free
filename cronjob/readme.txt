This folder is protected by htaccess -> browsers cannot access it.

You have to setup the cronjob so that it calls the script "cronjob.php" directly and not via http. 

The cronjob must run on the first day of the month so it can save the scores as YYYY-MM-01.

- - - - - - -

But if the cron job executes a web browser or something like wget, making an http request through the webserver, then the htaccess is preventing access.

If you NEED cronjob called via http, use something like: 

<Files "cronjob.php">
  Order deny,allow
  Allow from name.of.this.machine
  Allow from another.authorized.name.net
  Allow from 127.0.0.1
  Deny from all
</Files>

- - - - - - -

The "cronjob.php" copies the recent userpoints to the table qa_userscores *only* if the month does not exist yet in table 'qa_userscores'.

Set this in cpanel:
Minute: 0
Hour: 0
Day: 1
Month: *
Weekday: *
Command: /your-ftp-path/qa-plugin/best-users-per-month/cronjob/cronjob.php

* stands for every month.

- - - - - - -

You can also call the cronjob.php manually each month if you like (without cronjob). 
For that you have to remove the htaccess from the cronjob-folder or your browser says "access forbidden". 

- - - - - - -

IMPORTANT: 

If your table is not named "qa_userscores" please change the table name in file cronjob.php accordingly.

- - - - - - -

Good luck!
Kai | q2apro.com
