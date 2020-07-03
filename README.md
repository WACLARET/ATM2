docker-compose-laravel
A pretty simplified docker-compose workflow that sets up a LEMP network of containers for local Laravel development.
Usage
To get started, make sure you have Docker installed on your system, and then clone this repository.

First add your entire Laravel project to the src folder, then open a terminal and from this cloned respository's root run docker-compose up -d --build. Open up your browser of choice to http://localhost:8080 and you should see your Laravel app running as intended. Your Laravel app needs to be in the src directory first before bringing the containers up, otherwise the artisan container will not build, as it's missing the appropriate file.

New: Three new containers have been added that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command templates from your project root, modifiying them to fit your particular use case:

docker-compose run --rm composer update
docker-compose run --rm npm run dev
docker-compose run --rm artisan migrate
Containers created and their ports (if used) are as follows:

<ul>
<li>nginx - :8507</li>
<li>mysql - :3308</li>
<li>php - :9001</li>
<li>npm</li>
<li>composer</li>
<li>artisan</li>
  </ul>
Persistent MySQL Storage
By default, whenever you bring down the docker-compose network, your MySQL data will be removed after the containers are destroyed. If you would like to have persistent data that remains after bringing containers down and back up, do the following:

Create a mysql folder in the project root, alongside the nginx and src folders.
Under the mysql service in your docker-compose.yml file, add the following lines:
volumes:
  - ./mysql:/var/lib/mysql
