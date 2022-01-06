# Node.js OAuth 2.0 Quickstart

A quickstart app for integrators looking to use HubSpot's OAuth 2.0. Written in Node.js.

_**Note:** This app does not store any data in a persistent way, so restarting the app will clear the retrieved access tokens._

## What the app does

1. **Redirect to HubSpot's OAuth 2.0 server**

   When you open your browser to `http://localhost:3000/install`, the app will redirect you to the authorization page on
   HubSpot's server. Here you will choose which account you'd like to install the app in and give consent for it to act
   on your behalf. When this is complete, HubSpot will redirect you back to the app.

2. **Exchange an authorization code for access tokens**

   Now that you're back in the app, it will retrieve an access token and refresh token from HubSpot's server, using an
   authorization code that was supplied by HubSpot when you granted access to the app.

3. **Retrieve a contact**

   When the app has received an access token, it will redirect you to `http://localhost:3000/`. It will then use the access token to
   make a query to HubSpot's Contacts API, and display the retrieved contact's name on the page.
   

_**Note:** You must be a super-admin for the account that you want to install the app in._

## Option 1: Running locally using Node.js

1. Clone the repository:
   ```bash
   $ https://github.com/Hawkkkkk/sms-hubspot.git
   ```
2. Create a **`.env`** file in the root of the repository with the ID and secret for your app (found on the app settings page), eg:
   ```
   CLIENT_ID='xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
   CLIENT_SECRET='yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy'
   SCOPE='crm.objects.contacts.read,forms'
   ```
   You can also add a `SCOPE` environment variable to specify a custom set of scopes. The scopes can be separated by a comma, space, or URL-encoded space (`%20`)
3. From the root of the repository, run:
   ```bash
   $ yarn install
   $ yarn start
   ```
4. Open your browser to `http://localhost:3000/install` to kick off the OAuth 2.0 flow

---

## Option 2: Running in a Docker container

1. Build an image of the quickstart app

```
$ docker build -t sms:latest https://github.com/Hawkkkkk/sms-hubspot.git
```

2. Run a container with the new image

```
$ docker run --init -it -p 3000:3000 -e CLIENT_SECRET=$CLIENT_SECRET -e CLIENT_ID=$CLIENT_ID -e SCOPE=contacts,forms sms:latest
```
