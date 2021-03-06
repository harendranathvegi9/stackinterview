:heart: Stack Interview :blue_heart: 
===============
<img src="http://i.imgur.com/60VBQDL.png" align="right" margin="10px" padding="10px"> 

A RESTful API for web developer interview questions

This is an API that is constantly updated with the latest interview questions being asked by companies for front-end, back-end, and fullstack development jobs. It doubles as a quiz game on its own, allowing you to immediately test your knowledge. 

:notebook_with_decorative_cover: Table of Contents :notebook_with_decorative_cover:
=================
- [links](#links)
- [intro](#intro)
- [Installation](#installation)
- [Quiz game](#quiz-game)
- [API](#api)
  * [authentication](#authentication)
  * [reference](#reference)
  * [retrieving data](#retrieving-data)
  * [sending data](#sending-data)
- [Technologies](#technologies)
- [TODO](#todo)

=====

# :paperclip: links :paperclip:

[link to hosted project](https://stack-interview.herokuapp.com/login)

[wireframe](http://i.imgur.com/JcBVKwS.png)

[user stories](/userstories.md)

# :star2: Intro :star2:

Stack Interview is an API for the latest front-end and back-end interview questions being asked by employers around the world. 

As someone who will be looking for a job upon graduation very soon, I needed a way to quiz myself on important concepts and terms. I feel that this api and game will help developers reinforce things they've learned and reveal what needs to be studied further. There are so many new stacks, frameworks, and libraries popping up every week that it's hard to find a condensed source of core concepts to study. This project aims to ultimately encourage others to crowdsource a well-rounded pool of categorized information suitable for as many skill sets and skill levels as possible. 


# :hourglass_flowing_sand: Installation :hourglass_flowing_sand:
- fork or clone this repository down 
- `bundle install` & `bundle` 
- `rake db:create` & `rake db:migrate` & `rake db:seed` 
- `rails s`
- create user through pg or signup page to get and use an api_key 

# :game_die: Quiz Game :game_die:

<img src="http://i.imgur.com/LYl3pzy.png" width="396" height="605">

In order to visually display the API as an example I decided to make a quiz game. The icons at the top will filter the questions to display only certain stack-related questions. 

>NOTE: The game is not yet fully functional and only allows you to skip through the questions. Any other functionality shown below will be added in future releases. 

Click on one of the filter icons to choose which category of questions to see: 

<img src="http://i.imgur.com/3VGbVQA.png" width="90" height="90" float="left"> frontend

<img src="http://i.imgur.com/wCpAXGx.png" width="90" height="90" float="left"> backend

<img src="http://i.imgur.com/60VBQDL.png" width="90" height="90" float="left"> fullstack

The rest is pretty self-explanitory. Your score of right and wrong answers is at the top right and on the bottom right you can skip the current question. Logging out will end the current game. 

# :gift: API :gift:

## authentication

:lock: Stack Interview requires an API key for anything other than GET requests. 

Getting an API key is super easy though! Just [register an account](https://stack-interview.herokuapp.com/signup) and you will be redirected to it. The API supports both params and request headers 

####Headers

`curl -H 'X-API-Key: your-api-key" http://localhost:3000/api/v1/questions`

####Params

`curl http://localhost:3000/api/v1/questions&api_key=yourkeyhere`

## reference 

| property | description | type | example |
| ----------- | -------------- | ----------| ----------- | 
| id           | question id | integer | 22          |
| title | question title | string | "What's the M in MVC?" |
| answer | question answer | string | "model" | 
| rating | rating for quality of question between 1 and 5 | integer | 2 | 
| category | frontend or backend | string | backend | 
| keyword | hashtags before 2009 | string | pattern | 

## retrieving data

Filtering options 

| parameter | description | example | 
| -------------- | -------------- | ------------ | 
| category | retrieve questions from this category | &category=frontend | 
| keyword | retrieve questions with this keyword | &keyword=javascript | 
| rating | retrieve only questions with specific rating | &rating=4 | 
| min_rating | retrieves only questions with this rating or greater | &min_rating=3 | 
| title_includes | retrieve questions containing a certain word (ignores case) | &title_includes=javascript | 

__retrieve frontend questions related to javascript:__ 

`curl http://localhost:3000/api/v1/questions&api_key=yourkeyhere&category=frontend&keyword=javascript`


## sending data 

> :lock: __POST, PUT, PATCH, and DELETE require an API Key__

__JavaScript example of sending a POST request:__ 

```javascript
 $.ajax({
    type: "POST",
    url: "http://localhost:3000/api/v1/questions&api_key=yourkeyhere",
    dataType: "json",
    data: {
        title: title
        answer: answer
        rating: rating
        category: category
        keyword: keyword 
    },
    success: function(data){
      console.log(data);
    },
    error: function(err){
      console.log(err);
    }
  })
```

__JavaScript example sending a PATCH request with API key in headers__ 

```js 
  $.ajax({
    type: 'PATCH',
    url: 'http://localhost:3000/api/v1/questions/5',
    headers: {
        "X-API-Key": "your-api-key" 
    },
    dataType: 'json',
    data: {
        title: title
        answer: answer
        rating: rating
        category: category
        keyword: keyword 
    },
    success: function(data){
      console.log(data);
    },
    error: function(err){
      console.log(err);
    }
  })
```

# :floppy_disk: Technologies :floppy_disk:

Front-end: 
- Sass
- Backbone 

Back-end: 
- Rails
- Postgresql 

Notable gems: 
- 12factor 
- bcrypt 
- dotenv 
- rack-cors 

I chose rails over sinatra because it is the standard for RESTful APIs. More importantly, it has the ability to scale and mutate databases very easily out of the box. I know there will likely be multiple of this API so this felt like the right choice for a one-person operation. 

# :coffee::coffee::coffee: TODO :coffee::coffee::coffee:

Time constraints have left the quiz game as more of a minimal demo display than a game. I only had a few days to work on this as a class project but hope to pursue it further once time permits. 

## :rotating_light: Known Issues / Features To Be Added :rotating_light:

 __The quiz game does not currently work properly. The only button that works is the skip button.__
 
- [ ] Think of the best way to implement backbone views with the possible answers. Currently it does display the proper answer randomly sorted within one of the three choice views. 
- [ ] Add backbone filtering on the filter buttons.
- [ ] Add animations and page transitioning for a better experience 
- [ ] The score count needs to be implemented per session 

