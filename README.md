# Console Logs

### General Assembly Project 4

![Screenshot 2022-03-24 at 18 29 53](https://user-images.githubusercontent.com/91087641/160178949-e3c1156c-a150-49a1-b026-5ba882074490.png)

## Brief 

Build a **full-stack** application by making your own **backend** and your own **frontend**.

Use a **Python Django API** using **Django REST Framework** to serve your data from a **Postgres** database.

Consume your **API** with a separate **frontend** built with **React**.

Be a complete product which most likely means **multiple relationships** and **CRUD functionality** for at least a couple of **models**.

Have a **visually impressive design**

Group Project (3 People) 

Timeframe: 8 days

## Deployment

Repository link: https://github.com/PeterBid/Project-4

## Team

#### • [Peter Bid (Me)](https://github.com/PeterBid) 

#### • [Thor Refoy](https://github.com/thor-r)

#### • [Ali Ali](https://github.com/alibeniaminali)

## Concept

Console Logs is a Social Media Platform in which users can watch, review and upload media and video clips related to console and computer gaming. 

As fans of gaming generally, we were inspired by various aspects of Twitch, Steam and Youtube, wishing to combine these aspects together to build a visually striking and interactive gaming related video platform. 

This is a full-stack application built with Django REST Framework and React. It was also my first experience using Python and Django in the back-end.

The whole application was built over 8 days in a team of three devs.


## Installation

* Install back-end dependencies: `pipenv`
* Enter Shell for project: `pipenv shell`
* Make Migrations: `python manage.py makemigrations`
* Migrate: `python manage.py migrate`
* Load Seed data for Genres: `python manage.py loaddata genres/seeds.json`
* Load Seed data for Games: `python manage.py loaddata games/seeds.json`
* Load Seed data for Users: `python manage.py loaddata jwt-auth/seeds.json`
* Load Seed data for Medias: `python manage.py loaddata medias/seeds.json`
* Load Seed data for Comments: `python manage.py loaddata comments/seeds.json`
* Start back-end server: `python manage.py runserver`
* Change into front-end directory: `cd client`
* Install front-end dependencies: `yarn`
* Start front-end server: `yarn start`

## Technologies Used

#### Frontend

* React
* Axios
* React Bootstrap
* CSS
* SCSS

#### Backend

* Python
* Django
* Django REST framework
* PyJWT
* PostgreSQL
* Psycopg2

#### Development tools

* Visual Studio Code
* Insomnia
* Yarn
* Cloudinary
* Git & GitHub
* Google Chrome development tools
* Figma (wireframing frontend)
* FigJam (wireframing backend)
* Asana (planning and timeline)
* Canva (logo, images and gifs)

## Process

### Planning

After researcheing the basic layout of video sites such as Twitch and Youtube we made a wireframe for the front-end using `Figma`. 

For planning out how the backend would work, we decided that in order set genres for the games it would be easier to have a separate `Genre` model akin to searching by Tags. This way we could create a `many to many` relationship with games allowing users to filter games by genres on the front-end. 

We then made an `ERD` with `FigJam` to visualise the relationships between the different models.

An `Asana` Board was also created to keep track of our short term and long term objectives for the project.

#### Wire Frame

<img width="693" alt="Screenshot 2022-03-02 at 21 43 50" src="https://user-images.githubusercontent.com/91087641/160553299-a4830a60-4538-4def-9a02-6daa0aa65246.png">

#### ERD

<img width="1012" alt="Screenshot 2022-03-02 at 21 37 51" src="https://user-images.githubusercontent.com/91087641/160553366-37c945ec-a135-470c-b4b3-3807d41de73c.png">

### Creating the Back-end with Django





## Challenges and Wins

#### Challenges

#### Wins

## Future Improvements

## Key Learnings

## Contact

Social - www.linkedin.com/in/peter-bid

Email - peterbid21@gmail.com
