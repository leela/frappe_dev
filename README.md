# Setting Up Frappe Dev Instance Using Docker

## Prerequisites
* Docker
* Docker Compose

## Dev Instance - How To Start
Step 1: Clone the repositories
```
    $ git clone https://github.com/leela/frappe_dev.git
```

Step 2: Start the dev instance
```
    $ cd frappe_dev
    $ docker-compose up
```
It will be little slow for the first time as it needs to build all the services. 

Step 3: Create a new site
```
    $ docker-compose exec frappe bench new-site sitename 
```

You are ready to use the system for development.

## How to use bench 
You need to append `docker-compose exec frappe` to all your bench commands to execute.

Ex:
```
    $ docker-compose exec frappe bench get-app erpnext 
    $ docker-compose exec frappe bench --site test install-app erpnext 
```

## Where is the code
In a repo you will see a directory called `development` where your bench is mounted. This is your working directory, where you can modify and commit changes. 

## Docker Compose Basic Commands
### List the services running

```
leela@Leelas-Air frappe_dev % docker-compose ps
           Name                          Command               State     Ports
--------------------------------------------------------------------------------
frappe_dev_frappe_1           bench start                      Exit 0
frappe_dev_mariadb_1          docker-entrypoint.sh mysqld      Up       3306/tcp
frappe_dev_redis-cache_1      docker-entrypoint.sh redis ...   Up       6379/tcp
frappe_dev_redis-queue_1      docker-entrypoint.sh redis ...   Up       6379/tcp
frappe_dev_redis-socketio_1   docker-entrypoint.sh redis ...   Up       6379/tcp
```

### More Commands
* Start all the services or any particular service using the `start` command

    $ docker-compose start
    $ docker-compose start frappe

* Stop all the services or any particular service using the `stop` command
    $ docker-compose stop
    $ docker-compose stop frappe

* Restart all the services or any particular service using the `restart` command
    $ docker-compose restart
    $ docker-compose restart frappe

* Destroy the dev instance by using `down` command
    $ docker-compose down

* Build the services
    $ docker-compose build
    $ docker-compose build --no-cache
