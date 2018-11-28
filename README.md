<a id="top"></a>

# Book Share Pro

**Author**: Ben Hurst

**Version**: 0.1.0

___

## Table of contents
* [Overview](#overview)
* [Technologies Used](#technologies)
* [Getting Started](#gettingStarted)
  * [Clone Repo](#clone)
  * [Seed Database](#seed)
  * [Run Tests](#test)
  * [Start Server](#run)
* [API Endpoints](#endpoints)
* [Models](#models)
  * [Airport Model](#airport-model)
  * [Flight Model](#flight-model)
* [References](#references)
* [Change Log](#change-log)

___

<a id="overview"></a>
## Overview

* Book Share Pro is a Facebook-integrated web community where users can lend and borrow their personally owned books. Once logged in, users will have access to the shared book collections of all their Facebook friends registered on our site. Check-out requests and due date reminders are facilitated through an easy-to-use notification system.
* Featuring "Shelf Scan" - the web's only automatic book loading image recognition tool! By loading just a single photo of their book shelf, "Shelf Scan" will parse out the text from each book and automatically load each book to the user's personal collection.

___

<a id="technologies"></a>

* Book Share Pro is built using Django Web Framework and PostgreSQL. 
* The "Shelf Scan" tool leverages Google's Cloud Vision API along with various image processing and computer vision tools (NumPy, Matplotlib, OpenCV).

___
<a id="gettingStarted"></a>
## Getting Started in Development

<a id="setup"></a>
### Clone this repo and setup PostgreSQL

1. Clone this repository.
1. In the terminal, run ```cd final_project```
1. Run ```touch .env```
1. In the .env file, paste the appropriate environment variables (ask a team member).
1. In a separate terminal instance, run ```psql```
1. Run ```CREATE DATABASE book_share;```
1. Back in the main terminal instance, run ```pipenv shell```
1. Run ```pipenv install```

<a id="server"></a>
### Seed database and run server
1. Run ```./manage.py makemigrations```
1. Run ```./manage.py migrate```
1. Run ```./manage.py createsuperuser``` and follow the prompts to create an admin account.
1. Run ```./manage.py runserver```

<a id="oauth"></a>
### Configure Facebook OAuth Services
1. In your browser, navigate to ```localhost:8000/admin/``` and login with superuser credentials.
1. Under ```Sites``` click on ```Sites```
1. In the upper right, click on ```Add site +```
1. In the domain name field, type ```localhost:8000```. In the Display Name field, type ```Books Share```. Click ```Save```. On the top left, navigate back to ```Home```
1. On the admin console Home page, under ```Social Accounts```, click on ```Social Applications```. On this page, click on ```Add social application +```.
1. Under the provider dropdown, choose ```Facebook```.
1. In the ```Name``` field, type ```Books Share```.
1. In the ```Client id``` and ```Secret key``` fields, type in the App ID and App Secret from this app on ```https://developers.facebook.com/``` (ask a team member)

1. In the ```Sites``` field, select ```localhost:8000``` and click on the right arrow so it appears under ```Chosen sites```. Then click ```Save```.
1. Logout from the admin console.

<a id="site"></a>
### You're all set!
1. Navigate to ```localhost:8000```.
1. Login using FB Oauth.

___
<a id="endpoints"></a>
## API Endpoints


**GET** `/admin/`

***Client-side Usage:*** Access to the admin console (configure OAuth, direct CRUD operations to database)


