title: Docker
subtitle: Getting Started
-------

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Install AsgardCMS](#install-asgardcms)
- [Working with the containers](#working-with)
- [Xdebug](#xdebug)
- [Blackfire.io](#blackfireio)
- [Getting help](#getting-help)

## <a name="introduction" class="anchor" href="#introduction">Introduction</a>

Using Docker is a quick and easy way to run AsgardCMS in containers. By using Docker you will not need to install PHP, MySQL or a web server directly on your machine!

To get Docker installed, either read below or alternatively watch [Install AsgardCMS with Docker](https://www.youtube.com/watch?v=uZo5BHbv_lY).

## <a name="prerequisites" class="anchor" href="#prerequisites">Prerequisites</a>

To be able to run AsgardCMS under docker you will need:

- [Docker Engine (Community Edition)](https://store.docker.com/search?type=edition&offering=community)
- [Docker Compose](https://docs.docker.com/compose/install/)

## <a name="install-asgardcms" class="anchor" href="#install-asgardcms">Install AsgardCMS</a>

- [Install AsgardCMS](https://asgardcms.com/docs/v3/getting-started/installation)

### Database configuration

Docker will create a MySQL container with a new database for you automatically.

Be sure to set the database name, username, password you want to use in `docker-compose.yml`

### Run the containers

A helper tool called `dcp` exists in the root of the project. You may need to give it executable permissions before using it (`chmod +x ./dcp`).

Start the containers with this command.

``` .language-bash
./dcp up
```

If this is your first time running this command, it may take a little while to download/build the images.

### Run the install command

Now run the `./dcp artisan asgard:install` command to perform the AsgardCMS installation process.

When prompted for database credentials, use the details you specified in the `docker-compose.yml` file.

When asked for the **mysql host**, use the name of the mysql container from `docker-compose.yml` (by default `mysql`). 

### Enjoy

You can now login on `http://localhost/auth/login` with the email and password you entered during the install command. After you've logged in you'll be able to access the administration panel by visiting `http://localhost/backend`.

## <a name="working-with" class="anchor" href="#working-with">Working with the containers</a>

You will need to use the `./dcp` command when interacting with the container.

The most common commands you will need are:

- `./dcp`: Check the status of the containers
- `./dcp up`: Bring up the containers
- `./dcp down`: Stop the containers
- `./dcp rs`: Restart the containers
- `./dcp composer`: Run composer in the container
- `./dcp artisan or ./dcp art or ./dcp a`: Run the artisan command
- `./dcp test`: Run phpunit in a new container
- `./dcp t`: Run phpunit in the app container
- `./dcp yarn`: Run yarn
- `./dcp npm`: Run npm

For most of the above commands any arguments you enter after the command will be passed to the original command, for example running `./dcp artisan migrate` would run `php artisan migrate` and `./dcp test Modules/Core/Tests` would run PHPUnit for the Core module.

<div class="alert alert-success" role="alert">
	<strong>Tip!</strong> You can alias <code>./dpc</code> to <code>dpc</code>
</div>

### Rebuilding the image

Whenever you make a change to the `Dockerfile` files, you will have to rebuild the images for the changes to take effect. This can be done with:

- `./dcp build`
- `./dcp rs`

## <a name="xdebug" class="anchor" href="#xdebug">Xdeb
Xdebug is turned on by default and is configured for Docker For Mac.

To switch it off or adjust for a different platform, edit `/docker/app/enabled-xdebug.ini`.

After making xdebug changes, you will need to rebuild the images for the containers. Run `./dcp build` to rebuild the images, followed by `./dcp rs` to restart the containers.

## <a name="blackfireio" class="anchor" href="#blackfireio">Blackfire.io</a>

AsgardCMS docker setup comes with a [Blackfire.io](https://blackfire.io) container which contains the Blackfire Agent. The app container comes with the Blackfire probe set up by default.

To set it up, you need to fill in the server keys in `docker-compose.yml` file:

```.language-yaml
blackfire:
image: blackfire/blackfire
environment:
  BLACKFIRE_SERVER_ID:
  BLACKFIRE_SERVER_TOKEN:
networks:
- asgard_net
```


## <a name="getting-help" class="anchor" href="#getting-help">Getting help</a>

If you have **feedback** to give, **ideas** you would like implemented, by all means share them on the [forum](http://forum.asgardcms.com) in the "Comments and Feedback" section.

For **issues/bugs** you're having, you can use the Github Issues to post those. All issues are grouped on the [AsgardCms/Platform](https://github.com/AsgardCms/Platform/issues) repository.

If you just want to **talk**, join [our Slack channel (http://slack.asgardcms.com/)](http://slack.asgardcms.com/).
