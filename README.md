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

For planning out how the backend would work, we decided that in order set genres for the games it would be easier to have a separate `Genre` model akin to searching by Tags. This way we could create a `many to many` relationship with games allowing users to filter games by genres on the frontend. 

We then made an `ERD` with `FigJam` to visualise the relationships between the different models.

An `Asana` Board was also created to keep track of our short term and long term objectives for the project.

#### Wire Frame

<img width="693" alt="Screenshot 2022-03-02 at 21 43 50" src="https://user-images.githubusercontent.com/91087641/160553299-a4830a60-4538-4def-9a02-6daa0aa65246.png">

#### ERD

<img width="1012" alt="Screenshot 2022-03-02 at 21 37 51" src="https://user-images.githubusercontent.com/91087641/160553366-37c945ec-a135-470c-b4b3-3807d41de73c.png">

### Creating the Backend with Django

#### Folder Structure 

In the end, the folders of different apps on the back-end look like the below picture, and each folder has a similar structure to the comments folder.

<img width="161" alt="Screen Shot 2022-03-29 at 08 31 05" src="https://user-images.githubusercontent.com/91087641/160558065-b79baabc-2b4a-4fe6-8d43-2a633aace9db.png">

Each folder has its purpose:

* `games` – holds a many to many relationship with genres, with many medias attached to a single game.
* `genres` – forms a many-to-many relationship with games. Aimed to create store categories like "action," "fps," "platform"...
* `medias` – holds many relationships as each media is related to a game and owned by a user, however multiple users can comment on each media. While • the medias we used in the site was based around videoclips we set up the back-end to be applicable to images as well.
* `comments` – forms a many-to-one relationship with medias. Intended for users' reviews and comments.
* `jwt_auth` – intended for user model and authentication when registering or logging into the site.

#### Models 

We then created each model, set each field and added the relationships in as fields into the models. Afterwards creating a super user and using the Django admin site to check all the models had the correct input types.

<img width="833" alt="Screenshot 2022-03-25 at 11 39 53" src="https://user-images.githubusercontent.com/91087641/160562148-d29bb3e6-7947-4f05-9e9c-be3841688c55.png">

<img width="1094" alt="Screenshot 2022-03-25 at 11 33 28" src="https://user-images.githubusercontent.com/91087641/160562379-40e3d739-60c7-4e6a-96be-faa362b44b92.png">

#### Serializers

Afterwards we created serializers both common and populated by the other models they have a relationship with for each model.

For example the Media serilazers looked like this.

```javascript
from rest_framework import serializers # so we can extend django's model serializer
from ..models import Media

# Serializers
class MediaSerializer(serializers.ModelSerializer):
    class Meta:
        model = Media # specify the model the serializer needs to use
        fields = '__all__'    
```

```javascript
from comments.serializers.populated import PopulatedCommentSerializer
from .common import MediaSerializer
from jwt_auth.serializers.common import UserSerializer
from comments.serializers.populated import PopulatedCommentSerializer
from games.serializers.common import GameSerializer

class PopulatedMediaSerializer(MediaSerializer):
    owner = UserSerializer()
    comments = PopulatedCommentSerializer(many=True)
    games = GameSerializer()
```
#### Authentication

We created an authentication.py file using JSON Web Token and the Basic Authentication from the Django REST Framework. 

This also involved adding a validate function in the UserSerializer to check and hash the passwords of the users. 

After this we then created Register and Login views. 

<img width="927" alt="Screenshot 2022-03-25 at 11 49 35" src="https://user-images.githubusercontent.com/91087641/160572171-2a0b3234-9546-4e5d-9393-197d12bb3352.png">

#### Views

Every created app has several options in `views.py` for example in medias views.py: GET one media, GET all medias, POST one media, EDIT one media, DELETE one media.

After creating each view we then used `Insomnia` and the admin to check all relationships between models were correct and that we were receiving the correct JSON responses when reaching each end point

<img width="938" alt="Screenshot 2022-03-25 at 11 46 37" src="https://user-images.githubusercontent.com/91087641/160569286-3a4e6805-e70f-4293-97dc-5883882ee1b5.png">

![Screenshot 2022-03-24 at 19 17 05](https://user-images.githubusercontent.com/91087641/160569389-d38be994-2dab-40d9-a57f-472363e27a70.png)

### Creating the Frontend with React

#### Creating Components

We created a React app and connected to the database. We then created all the components that we were planning to use and connected them using the React Router DOM. We then created the elements that would made up each individual component.

#### Home

In order to streamline the user experience, we decided to incorperate the list of games into the home page as well. For displaying the games, after using a `get` axios request to receive the data we used the `map` method alongside `flexbox` to display the characters in a grid. 

<img width="877" alt="Screenshot 2022-03-25 at 12 02 21" src="https://user-images.githubusercontent.com/91087641/160580161-ff0db491-d481-433c-9b59-aacb1fe8e6aa.png">

* Filtering

As the games had multple fields we wished for users to search by, the name of the game and the genere tag attached to the game, we needed to create search bar that could filter by both fields. Eventually we settled upon using Regular Expression `RegExp` to overcome this problem.

A `useState` of `searchTerm` in conjunction with another `useState` of `setTagSearchTerm` was created alongside a text form targeting what users typed as a search term for game names and genres. This was then used to create a `RegExp` function to `filter` out results for the `map`.

<img width="750" alt="Screenshot 2022-03-25 at 12 02 34" src="https://user-images.githubusercontent.com/91087641/160580261-72814224-5ecf-4523-9edf-711cd42d80cf.png">

<img width="957" alt="Screenshot 2022-03-25 at 12 04 27" src="https://user-images.githubusercontent.com/91087641/160580390-3f5b7edb-d46d-4106-989a-c1e4af391dba.png">

<img width="971" alt="Screenshot 2022-03-25 at 12 04 35" src="https://user-images.githubusercontent.com/91087641/160580452-9161169f-bf4f-4e5f-9707-3289609f66ba.png">

#### ImageUpload, MediaUploadForm and Cloudinary working with Video

We had previously used Cloudinary to upload images in our previous projects, however this was the first time using Cloudinary with videos. 

Fortunately the process was very simillar and after familiarising ourselves with using Cloudinary API to make post requests and store images there, we were able to quickly adjust it to video. 

```javascript
export const ImageUploadField = ({ handleImageUrl, setFormData, value }) => {

  const handleUpload = async event => {
    const data = new FormData()
    data.append('file', event.target.files[0])
    data.append('upload_preset', 'du2ggxil')
    const res = await axios.post('https://api.cloudinary.com/v1_1/sei61cloud/video/upload', data)
    ageUrl(res.data.url)
  }
```

```javascript
Using the `video` tag with React in the Return we were also able to easily add other aspects for the users to interact with the video's automatically, such as play/pause, screen size, open in second window, playback speed etc. 

  return (
    <>
    {value ?
      <div>
        <video src={value} alt='uploaded' width="350" height="250" controls></video> 
      </div>
      :
      <>
        <label>Upload Your Log</label>
        <br></br>
        <input
          className="input"
          type="file"
          onChange={handleUpload}
        />
      </>
    }
  </>
  )
}
```


We then added a MediaUploadForm for users to upload the Media. They also have a `Boolean` field to select whether they are uploading an image or video.

![Screenshot 2022-03-24 at 18 43 39](https://user-images.githubusercontent.com/91087641/160584153-5c7fe402-4613-43e8-925b-be3419d754f8.png)

#### Register & Login

For registering we created a form where the user must choose a unique username, email, password, and confirm password before proceeding with the registration. If there is no user in the database with the existing username or email, the user is successfully registered.

Upon successful registration, the user is redirected to the login page. If the data entered is the same as the data stored in the database, the user is then redirected to the home page.

![Screenshot 2022-03-24 at 18 42 52](https://user-images.githubusercontent.com/91087641/160592909-0fd47c0b-1d27-4e41-847b-790b6d555c64.png)

![Screenshot 2022-03-24 at 18 41 39](https://user-images.githubusercontent.com/91087641/160593054-5a0564a7-d1d2-4d45-bcfc-b7cee41faf8d.png)

Upon successful registration, the customer is redirected to the login page. If the data entered is the same as the data stored in the database, the user is then redirected to the home page.

#### GameDetail and MediaDetail

We used the `id` of each game on the home page , to create a `gameID` which then used with `useParams` created links to the `GameDetail` component. If a user clicks on an individual game, they are redirected to a page with detailed information about that game. This was then used to return specific information related to each game.

In GameDetail this process was repeated to map through all the medias attached to each game. The previous step was then repeated again created individual `MediaDetail` pages when users clicked the title of video.

<img width="1015" alt="Screenshot 2022-03-25 at 12 01 48" src="https://user-images.githubusercontent.com/91087641/160589229-d389c008-db71-4de5-af62-01cb8c90af8f.png">

![Screenshot 2022-03-24 at 18 38 41](https://user-images.githubusercontent.com/91087641/160589893-952731b8-58f5-478b-b1af-2da5b3c03cc2.png)

<img width="923" alt="Screenshot 2022-03-25 at 12 06 37" src="https://user-images.githubusercontent.com/91087641/160589518-dda14550-7d1d-4639-9cea-6b0b8c621b94.png">

![Screenshot 2022-03-24 at 18 51 24](https://user-images.githubusercontent.com/91087641/160590102-802168df-b8d2-49f2-9464-c6524082a4a0.png)

#### Commenting on Media



## Challenges and Wins

#### Challenges

#### Wins

## Future Improvements

## Key Learnings

## Contact

Social - www.linkedin.com/in/peter-bid

Email - peterbid21@gmail.com
