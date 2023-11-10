# docker-laravel10-nginx

## Environment settings

1. Create the `.env` file by making a copy of `.env.example`.

```bash
    #Executed from the linux console
    sudo cp .env.example .env  
```
2. Fill in the values of each environment variable

```bash
    MYSQL_DATABASE=
    MYSQL_USER=
    MYSQL_PASSWORD=
    MYSQL_ROOT_PASSWORD=
```
3. Create a `src` folder where the code of your app will persist and give it permissions

```bash
    #Executed from the linux console
    sudo mkdir src
    sudo chmod 777 -R src
```
4. Give permission to the folder `docker_stack`.

```bash
    #Executed from the linux console
    sudo chmod 777 -R docker_stack
```
5. Run docker and build

```bash
    #Executed from the linux console
    docker compose up -d --build
```

## Run command line in container

To enter the php container console

```bash
    #Executed from the linux console
    docker compose run --rm php /bin/sh
```
Create laravel project via composer:

```bash
    #Executed from the linux console
    docker compose run --rm composer create-project laravel/laravel .
```
If access Forbidden

```bash
    #Executed from the linux console
    docker compose run --rm php /bin/sh

    and then - 

    chown -R laravel:laravel /var/www/html

    chmod -R 777 /var/www/html/storage
    chmod -R 777 /var/www/html/bootstrap/cache

```

Stop containers

```bash
    #Executed from the console
    docker-compose stop

```

Stop and delete containers

```bash
    #Executed from the console
    docker-compose down

```
## Test app

Open the browser and enter http://localhost:8081

# Considerations

If you modify port values, verify where it is used and change it otherwise it will not work correctly.

If you already have docker containers, verify not to use the same local ports in order not to have conflicts, in case you want to use the same ones, those containers must be turned off when using this one.