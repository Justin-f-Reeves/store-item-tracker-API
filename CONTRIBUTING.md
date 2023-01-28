# CONTRIBUTING

## How to run the Dockerfile locally
```
docker run -dp 5000:5000 -w /app -v "$(pwd):/app" db-migrations sh -c "flask run --host 0.0.0.0"
```

> docker run -dp 5000:5000
runs the container as a daemon in the background, with port forwarding from 5000 to 5000.

> -w /app -v "$(pwd):/app"
sets up volume to sync local code to container's code

> db-migrations
just the name of the latest Docker image namded such simpy b/c this is where migrations were added.

>  sh -c flask run --host 0.0.0.0
tells the container not to run the CMD line of the Docker file, but rather instead run "flask run" and the location "--host 0.0.0.0"

Note that since Flask will now be handling the application server tasks instead of Gunicorn, the Flask environment variable settings in .flaskenv (e.g. Flask Debugger = 1) will kick in and you'll be able to have the app auto-restart when changes are made. 


## Connecting to Database 
The app should be connected to a PostgreSQL DB. 

Add a .env file to the top level of the directory from where the app is run and include a `DATABASE_URL` environment variable there as seen in `.env.example`, along with your own connection string. Note that some DB hosting services such as ElephantSQL may give you a connection string with older protocols that are now depricated by SQlAlchemy - be sure the connection string starts with `postgresql://`. 

