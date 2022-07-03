# MariaDB and DBeaver Setup Guide
A guide to install [MariaDB](https://mariadb.org/) and connect it to [DBeaver](https://dbeaver.io/) on Linux Manjaro.

## Why?
After struggling myself on this topic I decided to create this guide which gathers various resources found on the web, and share it in the name of helping my future self - and possibly others - who might be facing the same issues.

## Disclaimer
As already mentioned, I put this guide together by gathering various resources mentioned at the [bottom of this document](#useful-links).\
You're very encouraged to report incorrectness in case you find any.\
This guide comes with absolutely no warranty.

## DBeaver vs MySQL Workbench
I decided to go with [DBeaver](https://dbeaver.io/) as it proved to be stable on my machine.
[MySQL Workbench](https://www.mysql.com/products/workbench/) on the other hand would crash 9 times out of 10, so I decided to save myself some time and go with the former.

## Installation

Open a new terminal and install MySQL via [pacman](https://wiki.archlinux.org/title/pacman)

`sudo pacman -S mysql`

You are prompted with two options. Choose `mariadb` repository extra as mysql provider by pressing Enter or manually entering `1`.

You can now start MariaDB

`sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`

And execute *mysql_secure_installation* shell script

`sudo mysql_secure_installation`

See following screenshot as reference to determine which actions to perform - or see the original documentation [here](https://mariadb.com/kb/en/mysql_secure_installation/)

![mysql_secure_installation](https://user-images.githubusercontent.com/59341503/177056200-12f29eae-5647-4023-a1d5-0c4df79cad09.png)

In the original documentation [comments section](https://mariadb.com/kb/en/mysql_secure_installation/#comment_4085), some users warn about a missing step:

```
You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
... skipping.
```

When you're done, get inside MariaDB service

`sudo mariadb`

Or alternatively

`mysql -u root -p`

You can run all the commands you want here

`create database <dbtest_name>;`

`show databases;`

It's now necessary to grant user permissions

`GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY '<your_password>' WITH GRANT OPTION;`

And apply the changes

`FLUSH PRIVILEGES;`


Download DBeaver via Add/Remove Software and open it.\

Click Database > New Database Connection > Select MariaDB and hit Next

![mariadb-modal](https://user-images.githubusercontent.com/59341503/177056508-f96f01a0-2c01-4d49-80a3-4204fdf83ab8.png)

Hit the Finish button and you're set!

You should now see your DB named localhost inside Database Navigator tab

![db-navigator](https://user-images.githubusercontent.com/59341503/177056523-c3b6d4b6-40a8-4bbd-820e-96b9815bd353.png)

## Useful links
https://www.youtube.com/watch?v=fwGJukksL9w \
https://www.youtube.com/watch?v=DtRXOoQwdxY&t=444s \
https://mariadb.com/kb/en/mysql_secure_installation/ \
https://stackoverflow.com/questions/50453078/unable-to-connect-to-mariadb-using-dbeaver
