# Deploy `json-server` to `{{ free hosting site }}`

> Instructions how to deploy the full fake REST API [json-server](https://github.com/typicode/json-server) to various free hosting sites. Should only be used in development purpose but can act as a simpler database for smaller applications.

* [**Create your database**](#create-your-database)
* [Deploy to **Heroku**](#deploy-to-heroku)


## Create your database

1. Press the green `Use this template`-button in the right corner
2. Give your new repo a name and press the green `Create repository from template`-button
3. Clone your newly created repository to your computer

4 . Change the contents of `db.json` to **your own content** according to the [`json-server example`](https://github.com/typicode/json-server#example) and then `commit` your changes to git locally.

_this example will create `/posts` route , each resource will have `id`, `title` and `content`. `id` will auto increment!_
```json
{
  "posts":[
    {
      "id" : 0,
      "title": "First post!",
      "content" : "My first content!"
    }
  ]
}
```

---

## Deploy to **Heroku**
<a href="https://heroku.com/deploy?template=https://github.com/eecs130/json-server-heroku/tree/master">
    <img src="https://www.herokucdn.com/deploy/button.svg" alt="Deploy">
</a>

Heroku is a free hosting service for hosting small projects. Easy setup and deploy from the command line via _git_.

###### Pros

* Easy setup
* Free

###### Cons

* App has to sleep a couple of hours every day.
* "Powers down" after 30 mins of inactivity. Starts back up when you visit the site but it takes a few extra seconds. Can maybe be solved with [**Kaffeine**](http://kaffeine.herokuapp.com/)

---

### Install Heroku

1 . [Create your database](#create-your-database)

2 . Create an account on <br/>[https://heroku.com](https://heroku.com)

3 . Install the Heroku CLI on your computer: <br/>[https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)

4 . Connect the Heroku CLI to your account by writing the following command in your terminal and follow the instructions on the command line:
```bash
heroku login
```

5 . Then create a remote heroku project, kinda like creating a git repository on GitHub. This will create a project on Heroku with a random name. If you want to name your app you have to supply your own name like `heroku create project-name`:
```bash
heroku create my-cool-project
```

6 . Push your app to __Heroku__ (you will see a wall of code)
```bash
git push heroku master
```

7 . Visit your newly create app by opening it via heroku:
```bash
heroku open
```

8 . For debugging if something went wrong:
```bash
heroku logs --tail
```

---

#### How it works

Heroku will look for a startup-script, this is by default `npm start` so make sure you have that in your `package.json` (assuming your script is called `server.js`):
```json
 "scripts": {
    "start" : "node server.js"
 }
```

You also have to make changes to the port, you can't hardcode a dev-port. But you can reference herokus port. So the code will have the following:
```js
const port = process.env.PORT || 4000;
```
