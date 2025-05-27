# Postgres installation

This guide provides step-by-step instructions to install PostgreSQL 16 on Ubuntu 24.04, tailored for software developers. It uses the official PostgreSQL repository to ensure you get the exact version required.

## Prerequisites

- Ubuntu 24.04 (Noble Numbat) installed.
- Sudo privileges for the user.
- Internet connection to download packages.

## Installation Steps

1. Add the PostgreSQL APT Repository
    
Ubuntu’s default repositories may not include PostgreSQL 16, so add the official PostgreSQL APT repository for the latest version.
    
``` bash
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```
This command creates a new APT source file for PostgreSQL, targeting the Ubuntu codename (e.g., noble for 24.04).

2. Import the Repository Signing Key

Add the PostgreSQL GPG key to verify the authenticity of the packages.

``` bash
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

3. Update the Package Index

Refresh the APT package index to include the PostgreSQL repository.

``` bash
    sudo apt update
```

4. Install PostgreSQL 16

Install PostgreSQL 16 and the client tools.

``` bash
sudo apt install postgresql-16 postgresql-client-16
```

This installs the PostgreSQL 16 server and client utilities. The postgresql-client-16 package includes tools like psql for interacting with the database.

5. Verify the Installation

Check if the PostgreSQL 16 service is running.

``` bash
sudo systemctl status postgresql@16-main
```

Expected output should include active (running). If the service is not running, start it with:

``` bash
sudo systemctl start postgresql@16-main
```

Ensure PostgreSQL starts on boot:

``` bash
    sudo systemctl enable postgresql@16-main
```

6. Access PostgreSQL

PostgreSQL creates a default postgres user. Switch to this user to access the database.

``` bash
    sudo -u postgres psql
```

This opens the psql prompt. You can verify the version with:

``` sql
    SELECT version();
```

7. Optional: Create a New Database

To create a new database for your project, run in the psql prompt:

``` sql
    CREATE DATABASE myprojectdb;
```

Exit the psql prompt with:
\q

### Post-Installation Notes

- Configuration Files: PostgreSQL configuration files are located in `/etc/postgresql/16/main/`. 
    Key files include:
        - postgresql.conf: Main configuration file.
        - pg_hba.conf: Client authentication settings.


- Data Directory: The default data directory is `/var/lib/postgresql/16/main/`.

- Remote Access: To enable remote connections, modify `postgresql.conf` (set listen_addresses = '*' or specific IPs) and update `pg_hba.conf` to allow your client’s IP range. 
    Restart the service after changes:
    
``` bash
    sudo systemctl restart postgresql@16-main
```

- User Management: Create additional users with:

``` sql
CREATE USER myuser WITH ENCRYPTED PASSWORD 'mypassword';
GRANT ALL PRIVILEGES ON DATABASE myprojectdb TO myuser;
```

### Troubleshooting

- If apt update fails, verify the repository URL and GPG key.
- If the service doesn’t start, check logs in /var/log/postgresql/ for errors.
- Ensure port 5432 (default) is open if configuring remote access.
