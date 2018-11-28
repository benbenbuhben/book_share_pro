<a id="top"></a>

# Book Share Pro



**Author**: Ben Hurst

**Version**: 0.1.0

<a id="overview"></a>

### Overview

Book Share Pro is a Facebook-integrated web community where users can lend and borrow their personally owned books. Once logged in, users will have access to the shared book collections of all their Facebook friends registered on our site. Check-out requests and due date reminders are facilitated through an easy-to-use notification system.
* Featuring "Shelf Scan" - the web's only automatic book loading image recognition tool! By loading just a single photo of their book shelf, "Shelf Scan" will parse out the text from each book and automatically load each book to the user's personal collection.

___

## Table of contents
* [Overview](#overview)
* [Technologies Used](#technologies)
* [Getting Started](#gettingStarted)
  * [Clone repo and setup PostgreSQL](#setup)
  * [Seed database and run server](#server)
  * [Configure Facebook OAuth Services](#oauth)
  * [You're all set!](#site)
* [API Endpoints](#endpoints)
* [Models](#models)
  * [Profile Model](#profile-model)
  * [Book Model](#book-model)
  * [Document Model](#document-model)
  * [Notification Model](#document-model)

___

<a id="technologies"></a>

## Technologies Used

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
## Primary API Endpoints

**GET** `/`

***Description:*** Renders homepage view.

**GET** `/admin/`

***Description:*** Access to the admin console (configure OAuth, direct CRUD operations to database)

![Admin Console](/docs/admin_screenshot.png)

**GET** `/accounts/`

***Description:*** Various endpoints provided by Django-allauth - an integrated set of Django applications addressing authentication, registration, account management as well as 3rd party (Facebook) account authentication.

**GET** `/add/`

***Description:*** Add to your collection landing page.

**GET** `/add/search/`

***Description:*** Standard Google Books API search view.

**POST** `/add/search/`

***Description:*** Form submission ('query' key/value in POST body) to Google Books API.

**POST** `/add/post/`

***Description:*** Creates book model instance with foreign key relationship to user's profile.

**GET** `/add/scan/`

***Description:*** Renders "Shelf Scan" view.

**POST** `/add/scan/`

***Description:*** Passes uploaded shelf image through Book Spine Extraction pipeline.
___
<a id="models"></a>
## Models

<a id="profile-model"></a>

### 1. Profile Model
    Profile{
      user              foreign key
      username          string
      email             string
      first_name        string
      last_name         string
      fb_id             string
      picture           url
      friends           array
    }

<a id="book-model"></a>

### 2. Book Model

    Book{
      user	            foreign key
      owner             string
      borrower          string
      requester         string
      title             string
      author            string
      image_url         url
      year              string
      status            string
      data_added        datetime
      last_borrowed     datetime
      pre_save_status   datetime
    }
        
<a id="document-model"></a>

### 3. Document Model
    Document{
      user	            foreign key
      docfile           file
    }

<a id="notification-model"></a>

### 4. Notification Model
    Notification{
      type              string
      status            string
      from_user         string
      to_user           string
      date_added        string
      book_id           string
    }
    
[Back to top](#top)

