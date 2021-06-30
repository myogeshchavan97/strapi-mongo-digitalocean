# Strapi application

A quick description of your strapi application

# How to Configure Strapi with MongoDB and Deploy it on DigitalOcean Platform

### Introduction

In this tutorial, you will configure Strapi with MongoDB Atlas and deploy it to the DigitalOcean platform.

By doing this, you will understand:

- How to use Strapi as a headless CMS
- How to configure it locally first to test its functionality
- How to setup connection between Strapi and MongoDB Atlas so all the data will be stored in the database
- How to use environment variables to secure private database information in Strapi
- How to deploy Strapi configured with MongoDB to the DigitalOcean platform

By the end of this tutorial, you will have a complete Strapi + MongoDB database configured and deployed to DigitalOcean.

## Prerequisites

You will need the following to complete this tutorial:

- A [DigitalOcean](https://digitalocean.com/) account.
- A [GitHub](https://github.com/) account.
- A text editor. You can use [Visual Studio Code](https://code.visualstudio.com/download) or your favorite text editor.
- A valid Git installation. To set this up, review the [Getting Started with Git](https://www.digitalocean.com/community/tutorials/how-to-contribute-to-open-source-getting-started-with-git) tutorial.
- Node.js installed locally, which you can do by following the [How to Install Node.js and Create a Local Development Environment](https://www.digitalocean.com/community/tutorial_series/how-to-install-node-js-and-create-a-local-development-environment) tutorial.

This tutorial was verified with Node v14.16.0, npm v6.14.11.

### MongoDB Atlas Setup

This project also requires a [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account.

After creating an account and signing in, [follow these steps to deploy a free tier cluster](https://docs.atlas.mongodb.com/getting-started).

Once you have set a cluster, a database user, and an IP address you will be prepared for later acquiring the connection string as you set up the rest of your project.

> Make sure to keep a note of the database user name and password you created as it will be required later.

## Step 1 — Installing Strapi Locally and Configuring with MongoDB Atlas

In this step, you will set up a new Strapi project on your local machine.

To install Strapi locally, run the following command from your project folder.

```command
npx create-strapi-app strapi-mongo-digitalocean
```

Here, `strapi-mongo-digitalocean` is the name of the project you will be creating.

Once you execute the above command, you will be asked to choose the installation type.

![Select Installation Type](https://i.imgur.com/o36wN9h.png)

To navigate between the options, use the up and down arrow keys on the keyboard and select the `Custom (manual settings)` option by pressing the enter key.

Then you will be asked If you want to use a template?

![Select Template](https://imgur.com/hLowcYt.png)

Enter the value `n` to say `No` and press enter key.

Then you will be asked to select your default database client.

![Default Database Client](https://imgur.com/EGS3eAf.png)

Select the `mongo` option by using up and down arrow keys and press the enter key.

Then you will be asked to enter the database name.

![Database Name](https://imgur.com/3fcuIJF.png)

Press enter key to select the `strapi-mongo-digitalocean` as the database name.

Next, you will be asked to enter Host.

![Enter Host](https://imgur.com/1um7cho.png)

To find out the value for the host, log in to your MongoDB Atlas account and click on the `COLLECTIONS` button.

![Click Collections Button](https://i.imgur.com/fQcEqn3.png)

Next, click on the `Create Database` button.

![Create Database](https://i.imgur.com/70vwe2U.png)

Enter `strapi-mongo-digitalocean` as the database name and also as collection name and click on the `Create` button.

![Enter Database Name](https://i.imgur.com/4mdkPE8.png)

Click on the `Clusters` menu in the left navigation to go back to the Clusters overview page.

![Clusters Menu](https://imgur.com/4FPDsaV.gif)

Now, click on the `CONNECT` button which is displayed before the `METRICS` button in the Clusters section.

Then click on the `Connect your application` option:

![Connect Application](https://i.imgur.com/LHKQkSj.png)

You will see a connection string as shown in the below screenshot:

![Connection URL](https://i.imgur.com/kQFn1gz.png)

Copy the host value which is displayed after the `@` symbol up to the `/`. So in this case, the host value is `cluster0.ltzir.mongodb.net`.

Paste the copied value as the `Host` value in the terminal.

Then you will be asked for the `+srv` connection value.

![Enter Srv Connection](https://imgur.com/82W7RmO.png)

Enter `true` as the value and press enter key.

Then you will be asked to enter the Port.

![Enter Port](https://imgur.com/Y2RviF0.png)

Enter `27017` as the value for port and press enter key.

Then you will be asked the `Username` and `Password` for the user which you have created while following the [MongoDB Atlas Setup](#mongodb-atlas-setup) step above.

![Enter username](https://imgur.com/F8P7lN8.png)

Enter those values of username and password.

Then you will be asked `Authentication database`.

![Authentication Database](https://imgur.com/ki0mTlt.png)

Don't enter anything. Just press the enter key.

Then you will be asked whether to enable SSL connection.

![Enable SSL](https://imgur.com/dWwYFwZ.png)

Enter the value `y` to say `yes`.

After entering all these details, wait for some time and your Strapi project will be created.

![Project Created](https://imgur.com/JxEW0a4.png)

## Step 2 — Running the Strapi Project

In this step, you will see how to start the Strapi Project and create a new admin user account.

Use the `cd` command to change the directory and go inside the `strapi-mongo-digitalocean` folder by running the following command:

```command
cd strapi-mongo-digitalocean
```

Next, start the development server by running the following command:

```command
npm run develop
```

The first time when you run this command it will take some time as it will build the Admin UI with our provided configuration changes.

And once it's done you will be automatically redirected to `http://localhost:1337/admin/auth/register-admin` URL in a web browser and you will see the screen similar to as shown below:

![Register Admin Account](https://i.imgur.com/6QDR5I0.png)

Create a new admin user by entering all the details and click on the `LET'S START` button.

> Make a note of the email and password you're entering because you will need that information to log in every time your restart the server.

Once done, you will be presented with the dashboard page as shown below:

![Strapi Logged In Dashboard](https://i.imgur.com/SdE1Gsj.png)

## Step 3 — Defining Content Types and Adding data

In this step, you will define the type of content to add to MongoDB.

Click on the `CREATE YOUR FIRST CONTENT-TYPE` button to create a new Collection type in MongoDB.

You will see the screen similar to as shown below:

![Enter Collection Type](https://i.imgur.com/tFxXEN6.png)

Enter `Product` for the `Display name` and click on the `Continue` button.

![Select Field Type](https://i.imgur.com/csxmnjx.png)

Select `Text` for the field type and enter `title` value for the `Name` and click on the `Finish` button.

![Title Field Type](https://i.imgur.com/kJbWpxo.png)

Now, click on the `Add another field` button as shown below:

![Add Another Field](https://i.imgur.com/rgMqrLb.png)

and click on the `Number` type as shown below:

![Add Number Type](https://i.imgur.com/hPjEbzn.png)

and enter `price` for the `Name` field and select `decimal` from the `Number format` dropdown and click on the `Finish` button.

![Enter price type](https://i.imgur.com/oy4rFEL.png)

Similarly, add another field with the name `quantity` of type `Number` and `integer` for the `Number format`.

![Enter Quantity Type](https://i.imgur.com/xTipLXu.png)

Once all three fields are added, click on the `Save` button.

![Save Content Types](https://i.imgur.com/tY2Uj0W.png)

Once saved, you will see the `Products` collection type added on the left side of the dashboard under the `COLLECTION TYPES` menu as shown below:

![Collection Types](https://imgur.com/ae7SVWa.png)

Once you click on the `Products` collection type on the left side, you will see a page to add new products as shown below:

![Add Products Section](https://i.imgur.com/pliCOgx.png)

Click on the `Add New Products` button displayed on the right side and enter the details of the product as shown below and click on the `Save` button.

![Adding Product](https://i.imgur.com/l6lJB2O.png)

Once saved, click on the `Publish` button to make the product available via REST API in case If you need it.

![Publish Product](https://i.imgur.com/eGerRGy.png)

Add some more products in a similar way and publish them and once done, you will see the `Products` section as shown below:

![Added Products](https://i.imgur.com/b2LcLNO.png)

## Step 4 — Verifying MongoDB Atlas for The Added Products

In this step, you will verify that the data added from Strapi is saved to the MongoDB Atlas.

Now, you have added products from the Strapi, so let's verify If the data is saved or not to the MongoDB Atlas database.

Login to your MongoDB Atlas account and click on the `COLLECTIONS` button displayed on the dashboard.

![Click Collections](https://i.imgur.com/fQcEqn3.png)

If you expand the `strapi-mongo-digitalocean` database, you will see that all the products are added to the `products` collection as shown below:

![Collection data in Atlas](https://i.imgur.com/E6lAekg.png)

So this confirms that, Strapi is correctly configured to connect to MongoDB Atlas account.

## Step 5 — Adding Environment Variables

In this step, you will see how to use environment variables to secure your database connection string, username and password.

Create a new `.env` file in the `strapi-mongo-digitalocean` project folder with the following content:

```js
DATABASE_HOST=
DATABASE_NAME=
DATABASE_USERNAME=
DATABASE_PASSWORD=
```

Provide the actual values for these environment variables after the `=` sign which we added while creating the Strapi App. You can find the values to enter in the `strapi-mongo-digitalocean/config/database.js` file.

Open the `config/database.js` file from the project. You will see all the configurations that you entered while creating the Strapi project.

Make the following changes in the file.

Change `host: env("DATABASE_HOST", "some_value")` to `host: env("DATABASE_HOST")` and

`database: env("DATABASE_NAME", "some_value")` to `database: env("DATABASE_NAME")` and

`username: env("DATABASE_USERNAME", "some_value")` to `username: env("DATABASE_USERNAME")` and

`password: env("DATABASE_PASSWORD", "some_value")` to `password: env("DATABASE_PASSWORD")`.

Here, we're telling Strapi to use the values of environment variables from the `.env` file instead of hardcoded values.

Your .env file will look like this now:

```
DATABASE_HOST=enter_your_database_host_here
DATABASE_NAME=strapi-mongo-digitalocean
DATABASE_USERNAME=enter_your_db_username
DATABASE_PASSWORD=enter_your_db_password
```

Now, stop the Strapi server and restart it by running the `yarn develop` command again, and If you refresh the page, you will see that the added data is correctly getting loadded as before after using values from the `.env` file.

## Step 6 — Deploying to DigitalOcean App Platform

In this step, you will see, how to push the locally configured Strapi App to GitHub and deploy it to the DigitalOcean App platform.

To deploy the App to DigitalOcean, we first need to create a Git repository and push the code to GitHub.

To initialize the Strapi project as a Git repository, run the following command from the `strapi-mongo-digitalocean` folder:

```command
git init .
```

Now, login to your GitHub account and create a new GitHub repository by visiting [this URL](https://github.com/new/).

Once the repository is created, copy the entire line displayed on your screen which says `git remote add` as shown in the below screenshot:

![Copy Add Remote URL](https://i.imgur.com/GzRMLyK.png)

Now, open the terminal and execute the copied command from your project folder.

This will make your local git repository point to the GitHub repository.

Now, execute the following command to add all code to the staging area:

```command
git add --all .
```

Commit all local changes by executing the following command:

```command
git commit -m "initial commit"
```

Push all the code to the GitHub repository by executing the following command:

```command
git push origin master
```

Now, log in to your [DigitalOcean account](https://cloud.digitalocean.com/) and click on the green `Create` button displayed at the top and select the `Apps` option from the menu.

![Create App](https://i.imgur.com/Bitn3Sj.png)

You will see the screen as shown in the below screenshot:

![Select Source](https://i.imgur.com/mJ1MFhx.png)

Click on the GitHub link and you will see the following screen:

![Choose Repository](https://i.imgur.com/BKFiMwi.png)

Click on the `Manage Authorization` link and give DigitalOcean permission to access your selected or all GitHub repositories.

![Search Repository](https://i.imgur.com/ybyzHU1.png)

Search and select the repository you want to deploy:

![Selected Repository](https://i.imgur.com/qG3IrIg.png)

Now, click on the `Install & Authorize` button and you will be redirected back to the `Choose Source` screen as shown below:

![Choose Source](https://i.imgur.com/mJ1MFhx.png)

Again click on the GitHub link.

From the dropdown choose the repository you selected in the previous step.

Keep the `Autodeploy code changes` button checked, so every time you push some code to your GitHub repository, it will be automatically deployed to DigitalOcean.

Now, click on the `Next` button.

![Choose Source Selection](https://i.imgur.com/RZhp4Hu.png)

In the next screen, keep the `Type` dropdown value as `Web Service` and click on the `Edit` link in front of the `Environment Variables` section to add environment variables.

![Add Environment Variables](https://i.imgur.com/bAo4uAb.png)

Add all the environment variables you created from the `.env` file of the project as key-value pairs.

Once done, click on the `Next` button.

Select the region which is nearest to you from the `Region` dropdown and click on the `Next` button.

![Region Selection](https://i.imgur.com/Oxztd5m.png)

Select the plan as per your need and click on the `Launch Basic App` button from the bottom of the page.

![Select Plan](https://i.imgur.com/3eVmhaj.png)

Wait until the deployment is going on.

![Deploying App](https://i.imgur.com/OQHoeyH.png)

Once the deployment is successful, you will see a deployment success message along with the URL of the deployed application.

![Deploy Success](https://i.imgur.com/a3zxmb7.png)

Once you click on that link, you will see the following screen:

![Strapi Home Page](https://i.imgur.com/kEeTKE7.png)

Click on the `Open the administration` button and enter the same admin credentials for the admin account which was created in Step 2 of this tutorial.

You will see that all your Product collection data is correctly loaded on the deployed site which we added on our local Strapi application.

![List of products](https://i.imgur.com/2xvjTKS.png)

This is because you've connected the Strapi app to the MongoDB Atlas database.

## Conclusion

In this tutorial, you have created an application with complete Strapi + MongoDB database configuration and deployed it to the DigitalOcean Platform.

**You can find the complete GitHub source code for this application in [this repository](https://github.com/myogeshchavan97/strapi-mongo-digitalocean)**.

If you’d like to learn more about Strapi, take a look at the [tutorials](https://strapi.io/tutorials) on the Strapi website.
