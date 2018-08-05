# BlockFlix
This is a Flask application that implements an DVD Rental company's online transaction processing (OLTP) application. This application implements a database schema similar to loosely modeled after MySQL's Sakila sample database.

This project is designed to be used in a [Full Stack Data Engineering](http://google.com) course.

## Learning Objectives
This project is a _teaching aid_ designed to help teach the following concepts:
* Implementing one-to-many, many-to-many relationships with Flask-SQLalchemy
* Seeding applications with synthetic data
* Implementing callbacks that interface with external systems (e.g. Apache Kafka)

## Application Features
As a teaching aid, this application implements a minimal number of features:
* User registration, login
* DVD inventory management systems


## Quickstart

First, set your app's secret key as an environment variable. For example,
add the following to ``.bashrc`` or ``.bash_profile``.

```
export BLOCKFLIX_SECRET='something-really-secret'
```
Run the following commands to bootstrap your environment ::
```
git clone https://github.com/mikeghen/blockflix
cd blockflix
pip install -r requirements/dev.txt
npm install
```
Next, make a database:
```
mysql> CREATE DATABASE blockflix_development;
```
Before running shell commands, set the ``FLASK_APP`` and
``FLASK_DEBUG`` environment variables:
```
export FLASK_APP=autoapp.py
export FLASK_DEBUG=1
```
Run the following to create database tables and perform the initial migration ::
```
flask db upgrade
```
Finally, run the development server with:
```
npm start
```

## Deployment
To deploy:
```
export FLASK_DEBUG=0
npm run build   # build assets with webpack
flask run       # start the flask server
```
In your production environment, make sure the ``FLASK_DEBUG`` environment
variable is unset or is set to ``0``, so that ``ProdConfig`` is used.


## Shell

To open the interactive shell, run ::
```
flask shell
```
By default, you will have access to the flask ``app``.


## Running Tests

To run all tests, run:
```
flask test
```

## Migrations

Whenever a database migration needs to be made. Run the following commands ::
```
flask db migrate
```
This will generate a new migration script. Then run ::
```
flask db upgrade
```
To apply the migration.

For a full migration command reference, run ``flask db --help``.


## Asset Management
Files placed inside the ``assets`` directory and its subdirectories
(excluding ``js`` and ``css``) will be copied by webpack's
``file-loader`` into the ``static/build`` directory, with hashes of
their contents appended to their names.  For instance, if you have the
file ``assets/img/favicon.ico``, this will get copied into something
like
``static/build/img/favicon.fec40b1d14528bf9179da3b6b78079ad.ico``.
You can then put this line into your header::
```
<link rel="shortcut icon" href="{{asset_url_for('img/favicon.ico') }}">
```
to refer to it inside your HTML page.  If all of your static files are
managed this way, then their filenames will change whenever their
contents do, and you can ask Flask to tell web browsers that they
should cache all your assets forever by including the following line
in your ``settings.py``::
```
SEND_FILE_MAX_AGE_DEFAULT = 31556926  # one year
```