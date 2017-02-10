# TastyTest
This is a project using Docker Compose to manage linked images for Rails,
PostgreSQL and an Nginx reverse proxy.

To build the application, change directory to the project root and run the
command.

	docker-compose build

This will create three docker images; one for Nginx, one for PostgreSQL and
one for Ruby with Rails and Node.js with ComfyMexicanSofa installed.

To initialize the CMS database, run this command

	docker-compose run rails db_init 

Once this is done, start the application with this command

	docker-compose up -d

A HTTP listener will be exported on port 80 of the hosting machine. SSL on
port 443 is not configured.

Note that all passwords for Comfy and PostgreSQL are unchanged from their
defaults. Do **not** run this in production without changing them.

To gracefully stop the application, use the command

	docker-compose down

Note that no separate storage is configured for the database. It will be
necessary to run the "db_init" step after every "down" and before the next "up",
or the Rails application will fail due to the database not being set up.
