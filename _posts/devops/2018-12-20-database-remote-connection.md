---
layout: post
title: "Database Remote Connection"
comments: true
categories: devops
---

## Database Remote Connection Postgresql
To enable remote access to PostgreSQL server follow the steps below:
1. Connect to the PostgreSQL server via SSH .

2. Add the following line to the end of /var/lib/pgsql/data/postgresql.conf file:
    ```
    listen_addresses = '*'
    ```
    If you can't find the postgresql.conf file you can run the command 
        
        "psql -U postgres -c 'SHOW config_file'";
2. Add the following line to the end of /var/lib/pgsql/data/pg_hba.conf file:

    ```
    host all all 203.0.113.2/32 md5
    ```

    203.0.113.2/32 is the remote IP from which connection is allowed. If you want to allow connection from any IP specify 0.0.0.0/0 .
    
    md5 is the authentication method, which requires the client to supply a double-MD5-hashed password for authentication.
    
3. Restart PostgreSQL server to apply the changes:

    ```
    service postgresql restart
    ```
    
#### Connect postgresql with Database tools

Here we have shown intellij database tools.

![Image](../../../../static/img/postgresql.PNG)
SSH configuration: 

Here user & password is the host machine User & Password 

![Image](../../../../static/img/postgresql.PNG)





