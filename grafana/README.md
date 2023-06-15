# Grafana
Here I am using docker-compose to run two containers, the app (Grafana) and the Data Base (Postgres).

First of all you will need to install Docker Compose, you can follow this official article https://docs.docker.com/compose/install/

After running the docker service, you can clone the files and set the environment variables with your own parameters.

Save the files and run Docker Compose in the same directory: docker-compose up -d.

If everything worked fine, you can now open your web browser, go to http://localhost:3000 and open Grafana for the first time.

# Tip

you can follow the container logs to see any errors or what's going on behind the scenes, using:

$ docker compose logs [OPTIONS] [SERVICE...]

- docker-compose logs -f grafana
- docker-compose logs -f postgres

Command to recreate only the specific container, in this case this command is useful because we don't want to recreate the database and lose the data (if you have already created dashboards, connectors or queries). If not, you'll need to back up the database before rebuilding everything.

$ docker-compose up --no-deps --build [OPTIONS] [SERVICE...]

- docker-compose up --no-deps --build -d grafana

# Problems solution

Sometimes you may see errors in grafana container to access the mapped folders, it is related to the user you are using to run docker-compose and the user specified for the docker-compoase.yml file.

- error
grafana_1 | t=2023-01-08T12:03:45+0000 lvl=eror msg="Problem reading image directory" logger=cleanup error="open /var/lib/grafana/png: permission denied"

To resolve this try specifying same user permissions for folder and docker-compose