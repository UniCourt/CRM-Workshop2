# CRM-Workshop 2 | Introduction MySQL and PHP

# CRM Workshop 2

One Day workshop on building containerized applications in PHP and MySQL.

## Prerequisite
---
### Any Linux machine/VM with following packages installed

- docker
- [docker-compose](https://docs.docker.com/compose/install/)
- git (any recent version)

### GitHub account
- Create an account on [GitHub](https://github.com/join) (Only if you do not have an account)
- Fork [this](https://github.com/UniCourt/CRM-Workshop1) repository and then clone it to your machine
- You can refer [this](https://docs.github.com/en/get-started/quickstart/fork-a-repo) guide to understand how to fork and clone



### Docker
- To install docker go to your cloned repository [CRM-Workshop1] and run the following command

    ``` sudo prerequisites_install_docker.sh ```

### Docker Images
- Run the following commands to get few docker images required for the workshop
    ```
    1. docker pull mysql:8.0
    2. docker pull php:7.4-apache
    3. docker pull hello-world
    4. docker pull alpine
    ```

### Workshop environment setup 
 - Check if Git, Docker, Docker Compose are installed and docker images are downloaded on the system. Open the terminal and run the following command

   ```
   Command: $ git --version
   git version 2.25.1

   Command: $ docker --version
   Docker version 20.10.17, build 100c701

   Command: $ docker-compose --version
   docker-compose version 1.25.0, build 0a186604

   Command: $ sudo docker images
   ```
## What will you learn by the end of this workshop?

- You will be able to operate and maintain databases in MySQL.
- You will be learn how to take advantage of relationships and internal consistency features of a Database.
- You will be able to use PHP's templating engine and build simple Server Side Applications.
- You will be able to write Object Oriented Programs in PHP
- You will be able to build dynamic web applications using PHP
- You will be able to persist and maintain application data on MySQL.
## Schedule
| Time            | Topics
|-----------------|-------
| 09:00 - 09:30   |  [`Introduction`]
| 09:15 - 12:00   |  [`Introduction to MySQL`](1.MySQL/1_create_table_with_contraints.md)
| 12:00 - 13:00   |  [`Introduction to PHP`](2_php/1_introducing_php.md)
| 14:00 - 16:00   |  [`Building Real World Applications with PHP`](2_php/6_httpd.md)
| 16:00 - 16:30   |  [`Wrapping Up`]
