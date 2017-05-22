---
layout: simple
title: Deploy a Client Application
category: lab
number: 2
---

## Clone the ice-client-app repo.

1. Launch a new browser tab.
2. Go to the [ice-client-app](https://github.com/fhakamine/ice-client-app) repo on Github.
3. On the top-right corner, click **Fork**.

## Launch the ice-resource-server app.

1. In the ice-client-app page, click the **Deploy to Heroku** button.
    You'll be redirected to Heroku.
2. Enter **ice-XXX** as App Name, replacing XXX with random numbers or letters of your choice.
3. Ignore the config variables for now (you'll change these properties with information from Okta later).
3. Click **Deploy**. Wait until the app is fully deployed.
4. Click **Manage App**.
5. Click **Open App**.
    The Ice Promos app is displayed in a new tab.

> #### Checkpoint
> At this point you have an API on the internet to display promotions plus a website that will consume the API calls. In the next section, you configure Okta to protect the promos Website.
