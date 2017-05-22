---
layout: simple
title: Deploy a Resource Server
category: lab
number: 1
---

## Log in or Sign up for Github, Heroku, and api.ai accounts

1. Go to [github.com](github.com) and login or sign up for a free account.
2. Launch a new browser tab.
3. Go to [heroku.com](keroku.com) and login or sign up for a free account.
4. Launch a new browser tab.
5. Go to [api.ai](api.ai) and login or sign up for a free account.
    At this point, you have three browser tabs logged in to github, heroku, and api.ai.

## Clone the ice-resource-server repo.

1. Launch a new browser tab.
1. Go to the [ice-resource-server](https://github.com/fhakamine/ice-resource-server) repo on Github.
2. On the top-right corner, click **Fork**.
    Github creates a repository under your account based on the ice-resource-server. This task may take few minutes.

## Launch the ice-resource-server app.

1. In the ice-resource-server page, click the **Deploy to Heroku** button.
    You'll be redirected to Heroku.
2. Enter **ice-rs-XXX** as App Name, replacing XXX with random numbers or letters of your choice.
3. Confirm that the App Name you entered is available and then click **Deploy**.
    Heroku will start the application deployment. This task may take few minutes.
4. Click **Manage App**.
5. In your App page, click the **More** > **View Logs**.
    Heroku displays the log for your app.
6. Launch a new browser tab, and then go to `https://<APP_NAME>.herokuapp.com/promos`. Replace `<APP_NAME>` to match your heroku app name.
7. You should see a JSON payload as follows:
    ``` json
    [
      {
        "code": "40OFFWEEK",
        "validFor": 7,
        "target": "PREMIUM",
        "created": "2017-05-15T18:29:26.042Z",
        "lastUpdated": "2017-05-15T18:29:26.042Z",
        "startDate": "2017-05-15T18:29:26.042Z",
        "endDate": "2017-05-22T18:29:26.042Z",
        "meta": {
          "revision": 0,
          "created": 1494872966044,
          "version": 0
        },
        "$loki": 1
      }
    ]
    ```

> #### Checkpoint
> At this point you have an API on the internet to display promotions. This API is not protected and can be accessed by any client on the internet. In the next section, you'll deploy a web app that will consume and this API.
