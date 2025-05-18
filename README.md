# Docker, Laravel, Nginx, MySQL8

How to create a Laravel project from scratch with Docker

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

4. Create a `frontend` folder where the code of your app will persist and give it permissions

```bash
    #Executed from the linux console
    sudo mkdir frontend
    sudo chmod 777 -R frontend
```

5. Give permission to the folder `docker_stack`.

```bash
    #Executed from the linux console
    sudo chmod 777 -R docker_stack
```

6. Run docker and build

```bash
    #Executed from the linux console
    docker compose up -d --build
```

## Run command line in container

To enter the php container console

```bash
    #Executed from the linux console
    docker compose run --rm php82 /bin/sh
```

To run npm, composer, artisan

```bash
    #Executed from the linux console
    #Replace "command" by the corresponding command, example docker compose run --rm php82 php artisan list
    docker compose run --rm npm "command"

    docker compose run --rm php82 composer "command"

    docker compose run --rm php82 php artisan "command"
```
## Create laravel 
Project via composer:

```bash
    #Executed from the linux console
    docker compose run --rm php82 composer create-project laravel/laravel .
```

## Create react 
use Docker to create the Vite project with React inside ./frontend

```bash
    #Executed from the linux console
    docker run -it --rm -v "$PWD/frontend":/app -w /app node:20-alpine sh

```

Inside the container frontend, execute:

```bash
    #Executed from the docker console
    npm create vite@latest . -- --template react

    # To exit the container.
    exit

```

Install the dependencies using Docker Compose:


```bash
    #Executed from the docker console
    docker compose run frontend npm install

```

After installation

```bash
    # Executed from the docker console
    docker compose up frontend
    # This will use
    command: sh -c "npm run dev"

```


If access Forbidden

```bash
    #Executed from the linux console
    docker-compose run --rm --user root php82 chown -R laravel:laravel /var/www/html

    # Executed from the linux console
    docker compose run --rm php82 /bin/sh

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
