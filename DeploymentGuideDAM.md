# Deployment Guide of the Data Administration Module

## Introduction

This document contains all the relevant information to deploy the application in a production environment.

First we start by describing our approach to decide how we were going deploy the application, then the steps to it.


### Our approach:
**Disclaimer**: There are many options to deploy the application, this document only describes one of them.

Initially we thought about using Docker to deploy the application, as it provided a unified way to deploy the application
in any environment.
However, we decided to not use Docker because we were having some problems running our application
in Docker, and, since this is a small application without many dependencies or environment specific configurations,
we decided to not use Docker.

It was decided that the application would be deployed in a Linux environment, as the requirement was to have an application
deployed in a cloud environment, DEI's cloud has plenty of Linux templates that we could choose to run our application.

**Selected machine**:
- **Operating System**: Alpine Linux v3.15 in a Linux container

We chose this machine based on the following reasons:
- It is a Linux machine, which is the environment we chose to deploy the application.
- It is a lightweight machine, which is good for a small application like ours.
- The version of the operating system allows us to easily install nodeJS (v16.14.2) and npm, being compatible with the
  application and python (v3.9) which is also required by the application (v3).
- It had the option to easily enable public SSH access, which helps to use bitbucket pipelines to deploy the application.
- It has a DNS name for an HTTP server running on port 80, which is useful to access the application.
- The cost of the machine on DEI's cloud is relatively low.

#### Selected deployment method:

Since we have our codebase on bitbucket, we decided to use bitbucket pipelines to help us with the automatic deploys.
Using bitbucket pipelines, we can easily have all the logic of building and deploying the application in a single place,
without having to worry about yet another tool to deploy the application.

Atlassian also has a student program, which
allows us to use up to 500 minutes of pipelines per month for free, and their documentation is very good.

**Pull-requests**:Our pipeline is configured to run on every pull request, running a build, the tests and linting, and, if everything
passes, then the reviewer has the information needed to review the pull request.

**Master**:When the pull request is merged, and the new code is on the master branch, the pipeline is triggered again,
but this time it builds the application, runs the tests and linting, and, if everything passes, it deploys the application to the server.

## Steps to deploy the application

In this topic we describe the steps and tricks to deploy the application.
Note that this guide is specific to the selected machine and deployment method, the steps may vary if you choose a different
machine or deployment method.

### 1. Create and start a new machine on DEI's cloud

Use the template number 10 "LAMP and others on Alpine Linux v3.15".

Use the option to create a VS from the template, and then start the VS.


### 2. Enable public SSH access to the machine

This step is required to allow bitbucket pipelines to access the machine and deploy the application.

You can enable public SSH access to the machine by going to the machine's page on DEI's cloud, and then clicking on the
"Enable" button referring to the "Public SSH/SFTP access" option.

### 3. Generate a new SSH key pair using bitbucket

Go on your repository settings --> SSH Keys and then click on "Generate keys".

Then, copy the public key and add it to your machine's authorized keys.
You can do this by copying the public key to the file `/root/.ssh/authorized_keys` on your machine.
Just enter on the end of the other keys, and paste it in a new line.

*Important*: Assure that the file is accessible by running the command `chmod 600 /root/.ssh/authorized_keys`.

### 4. Add your host to the known hosts on bitbucket

In the same menu as before, below the "Generate keys" button, there is a section called "Known hosts".

Add your host to the list of known hosts. Just copy your host's IP address/DNS name followed by the port of the public
SSH access you have (consult machine's page on DEI's cloud to know the port). and then click on "Fetch", once the "Add"
button appears, click on it, and it's done.

### 5. Create the deployment script

Create the file `deploy.sh` on the root of your repository, and paste the following content:

`````bash
#!/bin/bash

# Check if MongoDB URI is provided as an argument
if [ -z "$1" ]; then
  echo "Error: MongoDB URI not provided."
  exit 1
fi

# Change to the correct working dir
cd rdg-data-administration-module

# Update the code
git pull
echo "Git pull done"

# Install or update dependencies
npm install
echo "NPM install done"

# Set environment variables
export MONGODB_URI="$1"
export PORT=80

# Restart the application
npm run pm2:restart
echo "PM2 restart done"
`````

Make sure you give execution permissions to the file by running the command `chmod +x deploy.sh`.

### 6. Add the pipeline configuration to your repository

Go to your repository settings --> Deployment --> Production and add the following variables:

- **HOST_ADDRESS**: The IP address or DNS name of your machine.
- **HOST_PORT**: The port of the public SSH access you have (consult machine's page on DEI's cloud to know the port).
- **DB_CONNECTION_STRING**: The connection string to your database.

Create the file `bitbucket-pipelines.yml` on the root of your repository, and paste the following content:

`````yaml
pipelines:
  pull-requests:
     '**':
       - step:
           name: Build, Test & Lint
           image: node:18.18
           script:
             - npm install
             - npm test
             - npm run lint:fix
           caches:
             - node
  branches:
    master:
      - step:
          name: Deploy to VM
          deployment: production
          script:
            - pipe: atlassian/ssh-run:0.7.0
              variables:
                SSH_USER: 'root'
                SERVER: $HOST_ADDRESS
                PORT: $HOST_PORT
                COMMAND: "~/$BITBUCKET_REPO_SLUG/deploy.sh $DB_CONNECTION_STRING"
``````

### 7. Prepare the project to handle PM2

If you are going to deploy this application, all the configuration is already done (as the steps above describe too), but
for documentation purposes, we describe the steps to prepare the project to handle PM2.

First, why do we need PM2? PM2 is a process manager for NodeJS applications, it allows us to easily start, stop and restart
the application, and it also allows us to run the application in the background, so we can close the SSH connection to the
machine and the application will still be running.

This last feature is very important, because if we don't use PM2, the application will stop running when we close the SSH,
and in the case of the pipeline deployment we would have our pipeline running "forever", in this case until our
minutes of pipeline are over.

To prepare the project to handle PM2, we need to do the following steps:
- Install PM2 in the project: `npm install pm2`
- Configure the scripts in the `package.json` file:
    - Go to the `scripts` section and add the following scripts:
        - `"pm2:start": "pm2 start npm --name rdg-dam -- start"`
        - `"pm2:logs": "pm2 logs rdg-dam"`
        - `"pm2:list": "pm2 list"`
        - `"pm2:show": "pm2 show rdg-dam"`
        - `"pm2:stop": "pm2 stop rdg-dam"`
        - `"pm2:restart": "pm2 restart rdg-dam --update-env"`
        - `"pm2:delete": "pm2 delete rdg-dam"`

The most important scripts are the `pm2:start` and `pm2:restart`, as they are the ones that start and restart the application.
The other ones are just for convenience, to help us manage the application.

### 8. Deploy the application

Now the last step is to first clone the repository on the machine, and then run the command `npm run pm2:start` to start the
application.
Then you should push all your changes to the master branch so that the pipeline starts to deploy the new versions of the
application on every push to the master.

### Bonus

Before pushing the changes to the master, it's a good idea to test the whole process with the code still on the branch.
For this you do all the steps mentioned above, but before running pushing the code to the master, you checkout to the branch
where you are working, and then you run the command `npm run pm2:start` to start the application.

Then you can change something on the code, let's say, add a mock get route that returns "Hello World", and then you push
the changes to the branch, and then you go to the pipeline page on bitbucket, and you force a run of the pipeline with
the master configuration, and then you can see the pipeline running, and if the pipeline is successful, you can now test
if that new route is available on the application.