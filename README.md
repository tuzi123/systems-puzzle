# Insight DevOps Engineering Systems Puzzle

## Table of Contents
1. [Solution for the puzzle](README.md#Solution-for-the-puzzle)
2. [Problem introduction](README.md#Problem-introduction)


# Solution for the puzzle
1. Docker-compose ran properly, but the website cannot be accessed using `localhost:8080`. There might be some internet connection problem.
* In the `docer-compose.yml` file, fixed ports problem by changing to `ports: 8080:80`. Map port 80 in the container to port 8080 on the Docker host.
* In the `flaskapp.conf` file, fixed the nginx configuration problem by changing to `proxy_pass http://flaskapp:5000`. By default the app runs on port 5000. In the `app.py` file, the port number was specified as `app.run(host='0.0.0.0', port=5000)` to make it clear.
2. After fixing the connection problem, the website could be accessed successfully. The item information was entered to test the website functionality. After submitting the input data, an empty string was returned for each try. The `index.html`, `forms.py`, `models.py` and `app.py` were checked to fix this problem.
* In the `app.py`, the results were not returned properly. The data were returned successfully by using `render_template` with function return.
* In the `model.py`, the quantity was specified as Integer. However, in the `forms.py` the quantity was specified as String. Therefore `StringField` was replaced by `IntegerField` in the `forms.py` file. 

# Problem introduction

Imagine you're on an engineering team that is building an eCommerce site where users can buy and sell items (similar to Etsy or eBay). One of the developers on your team has put together a very simple prototype for a system that writes and reads to a database. The developer is using Postgres for the backend database, the Python Flask framework as an application server, and nginx as a web server. All of this is developed with the Docker Engine, and put together with Docker Compose.

Unfortunately, the developer is new to many of these tools, and is having a number of issues. The developer needs your help debugging the system and getting it to work properly.

## Puzzle details

The codebase included in this repo is nearly functional, but has a few bugs that are preventing it from working properly. The goal of this puzzle is to find these bugs and fix them. To do this, you'll have to familiarize yourself with the various technologies (Docker, nginx, Flask, and Postgres). You definitely don't have to be an expert on these, but you should know them well enough to understand what the problem is.

Assuming you have the Docker Engine and Docker Compose already installed, the developer said that the steps for running the system is to open a terminal, `cd` into this repo, and then enter these two commands:

    docker-compose up -d db
    docker-compose run --rm flaskapp /bin/bash -c "cd /opt/services/flaskapp/src && python -c  'import database; database.init_db()'"

This "bootstraps" the PostgreSQL database with the correct tables. After that you can run the whole system with:

    docker-compose up -d

At that point, the web application should be visible by going to `localhost:8080` in a web browser.

Once you've corrected the bugs and have the basic features working, commit the functional codebase to a new repo following the instructions below. As you debug the system, you should keep track of your thought process and what steps you took to solve the puzzle.
