# Docker, Laravel, Nginx, MySQL8

How to create a Laravel project from scratch with Docker

## Environment settings

1. Create the `.env` file by making a copy of `.env.example`.

```bash
    #Executed from the linux console
    sudo cp .env.example .env
```

2. Give permission to the folder `docker_stack`.

```bash
    #Executed from the linux console
    sudo chmod 777 -R docker_stack
```

3. Fill in the values of each environment variable

```bash
    MYSQL_DATABASE=
    MYSQL_USER=
    MYSQL_PASSWORD=
    MYSQL_ROOT_PASSWORD=
```

4. Create a `src` folder where the code of your app will persist and give it permissions

```bash
    #Executed from the linux console
    sudo mkdir src
    sudo chmod 777 -R src
```
5. Create React Frontend (Vite)

```bash
    #Executed from the linux console
    mkdir frontend

    sudo chmod 777 -R src

    docker run --rm -v "$PWD/frontend":/app -w /app node:20-alpine sh -c "npm create vite@latest . -- --template react"

    docker run --rm -v "$PWD/frontend":/app -w /app node:20-alpine sh -c "npm install"

```

5. Configure vite.config.js in frontend (if necessary)


```bash
    # Before running npm run dev, configure the vite.config.js file in the root directory of the frontend container. It should look like this
    import { defineConfig } from 'vite';
    import react from '@vitejs/plugin-react';

    export default defineConfig({
        plugins: [react()],
        server: {
            host: '0.0.0.0',
            port: 5173,
            strictPort: true
        },
        base: '/'
    });
    # This will use
    command: sh -c "npm run dev"
    # Executed from the docker console
    docker compose up frontend

```

5. Run docker and build

```bash
    #Executed from the linux console
    docker compose up -d --build
```

## Create Project  laravel 
With composer:

```bash
    #Executed from the linux console
    docker compose run --rm php82 composer create-project laravel/laravel .
```


If access Forbidden

```bash
    #Executed from the linux console
    docker compose run --rm --user root php82 chown -R laravel:laravel /var/www/html

    # Executed from the linux console
    docker compose run --rm php82 /bin/sh

    chmod -R 777 /var/www/html/storage
    chmod -R 777 /var/www/html/bootstrap/cache

```
## Test app

Open the browser and enter http://localhost:8081/ access the laravel project
Open the browser and access http://localhost:5173/ access the react project

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
# Considerations

If you modify port values, verify where it is used and change it otherwise it will not work correctly.

If you already have docker containers, verify not to use the same local ports in order not to have conflicts, in case you want to use the same ones, those containers must be turned off when using this one.
