## MySQL Compiled by Dan

[[https://github.com/dansnts/mysqlcompiled/blob/master/img/logo-mysql-170x115.png]]

MySQL Compiled for Arch users with x86_64 machines.

The same is compiled on my notebook through the MySQL AUR repository through the muflone maintainer PKGBUILD with the makepkg -s command.

Thanks muflone! Without your repository, maybe that would not be possible.

Advantages of using this repository: Save 1 hour or more (depending on your processor) to do other things.

### Attention
These packages conflict with Mariadb. If you have installed, uninstall.

### Instructions for use
1. Open your favorite terminal and go to the Downloads folder with the command:
```
cd ~/Downloads
```

2. Download the files for the installation:
* [**MySQL**](https://github.com/dansnts/mysqlcompiled/raw/master/files/mysql-5.7.21-1-x86_64.pkg.tar.xz)
* [**libmysqlclient**](https://github.com/dansnts/mysqlcompiled/raw/master/files/libmysqlclient-5.7.21-1-x86_64.pkg.tar.xz)
* [**MySQL Clients**](https://github.com/dansnts/mysqlcompiled/raw/master/files/mysql-clients-5.7.21-1-x86_64.pkg.tar.xz)

3. Check if the integrity of the files conforms to the file [SHA256SUM.txt](https://github.com/dansnts/mysqlcompiled/blob/master/files/SHA256SUM.txt)
```
MySQL: sha256sum mysql-5.7.21-1-x86_64.pkg.tar.xz
libmysqlclient: sha256sum libmysqlclient-5.7.21-1-x86_64.pkg.tar.xz
MySQL Clients: sha256sum mysql-clients-5.7.21-1-x86_64.pkg.tar.xz
```

4. Install the packages

```
sudo pacman -U mysql-5.7.21-1-x86_64.pkg.tar.xz libmysqlclient-5.7.21-1-x86_64.pkg.tar.xz mysql-clients-5.7.21-1-x86_64.pkg.tar.xz
```

When you finish installing the packages, the following alerts will appear:

```
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] 'NO_ZERO_DATE', 'NO_ZERO_IN_DATE' and 'ERROR_FOR_DIVISION_BY_ZERO' sql modes should be used with strict mode. They will be merged with strict mode in a future release.
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] 'NO_AUTO_CREATE_USER' sql mode was not set.
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] InnoDB: New log files created, LSN=45790
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] InnoDB: Creating foreign key constraint system tables.
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] No existing UUID has been found, so we assume that this is the first time that this server has been started. Generating a new UUID: {...}
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] Gtid table is not ready to be used. Table 'mysql.gtid_executed' cannot be opened.
dddd-dd-ddThh:mm:ss.milisecondsZ 0 [Warning] CA certificate ca.pem is self signed.
dddd-dd-ddThh:mm:ss.milisecondsZ 1 [Warning] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
```
This is normal because MySQL has not yet been configured. This will be done with the next steps.

5. Start MySQL server and autostart MySQL on boot:

```
systemctl start mysqld.service  ## use restart after update
systemctl enable mysqld.service
```

6. Configure the MySQL installation. As root user, type:

``` code
/usr/bin/mysql_secure_installation
```

Output:

```
Securing the MySQL server deployment.

Enter password for user root:
The 'validate_password' plugin is installed on the server.
The subsequent steps will run with the existing configuration
of the plugin.
Using existing password for root.

Estimated strength of the password: 100
Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y

New password:

Re-enter new password:

Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y
Success.

By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y
Success.

All done!
```

To remove the packages:

```
sudo pacman -Rscn mysql libmysqlclient mysql-clients

```

To update the version of MySQL, follow steps one through four again.

:smiley_cat: Thats all folks! :smiley_cat:
