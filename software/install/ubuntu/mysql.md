# MySQL installation

The mentioned steps were last tested on Ubuntu 24

## Step1

Update the package list

``` bash
sudo apt update
```

This command refreshes the local package index, allowing you to install the most recent version of MySQL available in Ubuntu 24’s repositories.

## Step2

``` bash
sudo apt install mysql-server
```

Install the MySQL server package, which includes everything needed to run a MySQL database server. During installation, the process may configure MySQL automatically and start the service. You might not be prompted for a root password at this stage, as recent versions of MySQL often use the auth_socket plugin by default for local root access.

## Step3

check whether mysql is installed or not

``` bash
mysql --version
```

## Step4

After installation, run the provided security script to configure essential security settings, such as setting a root password and removing unnecessary defaults.

``` bash
sudo mysql_secure_installation
```

This script will prompt you to:

- Set a root password: Choose a strong password type to be set when last time the script was executed and does not set the password directly.
- Remove anonymous users: Answer Y (yes) to eliminate unnamed accounts.
- Disallow remote root login: Answer Y unless you specifically need remote root access.
- Remove the test database: Answer Y to delete the default test database.
- Reload privilege tables: Answer Y to apply changes immediately.

## Step5

Try to log in as default root user

``` bash
sudo mysql
```

At this point no custom password is set for the `root` user.

## Step6

Reset the `root` user password using (note that you should be logged in using the `root` user before entering this steps)

``` sql
ALTER USER 'newuser'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

and exit from sql.

## Step7

Restart the mysql service

``` bash
sudo systemctl status mysql.service
sudo systemctl stop mysql.service
sudo systemctl start mysql.service
```

## Step8

Try to login as the root user using the password setup done in [Step6](#Step6)

``` bash
mysql -u root -p
``

If this did not work then google it out.
