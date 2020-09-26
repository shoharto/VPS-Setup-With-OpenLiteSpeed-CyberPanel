![nuxtjs-2](https://user-images.githubusercontent.com/23438431/94347848-5c4cc300-006a-11eb-9106-bc2284e39ad1.jpg)

# How to Deploy Nuxt JS on LiteSpeed Web Server
> Bayes Ahmed Shoharto

A brief description of Nuxt.js application deployment on LiteSpeed web server.

## Installing / Getting started

A quick introduction of the minimal setup you need to follow these steps:

<!-- - [Create Website](#Step-One)
- [Enable HTTPS](#Step-Two)
- [Connect to Server with SSH](#Step-Three)
- [Install Node JS & NPM](#Step-Four)
- [Upload Project File](#Step-Five)
- [Edit LiteSpeed Config File](#Step-Six)
- [Create .htaccess File](#Step-Seven)
- [Starting Nuxt.js](#Step-Eight)
- [Nuxt & PM2: Zero Downtime Deployment](#NUXT) -->



- [Step-One: Create Website](#step-one--create-website)
- [Step-Two: Enable HTTPS](#step-two--enable-https)
- [Step-Three: Connect to Server with SSH](#step-three--connect-to-server-with-ssh)
- [Step-Four: Install Node JS & NPM](#step-four--install-node-js---npm)
- [Step-Five: Upload Project File](#step-five--upload-project-file)
- [Step-Six: Edit LiteSpeed Config File](#step-six--edit-litespeed-config-file)
- [Step-Seven: Create .htaccess File](#step-seven--create-htaccess-file)
- [Step-Eight: Starting Nuxt.js](#step-eight--starting-nuxtjs)
- [Nuxt & PM2: Zero Downtime Deployment](#nuxt---pm2--zero-downtime-deployment)
- [Getting Started](#getting-started)
- [Configure your application](#configure-your-application)
- [Build and serve the app](#build-and-serve-the-app)

## Step-One: Create Website

Add new domain or subdomain in your LiteSpeed server by using web panel or terminal.

## Step-Two: Enable HTTPS

To know how to set SSL for HTTPS read this [SSL Documentation](CyberPanel/Configuration/SSL.md).

## Step-Three: Connect to Server with SSH 

To know how to connect to server by SSH for access read this [SSH Documentation](CyberPanel/Configuration/SSH.md).

## Step-Four: Install Node JS & NPM

To know how to install node.js and npm read this [Node.js Documentation](CyberPanel/Configuration/Node-js.md). 

## Step-Five: Upload Project File

Now go to your project directory:

```shell
cd /home/your-domain.com
```

And create directory for the project:
```shell
mkdir ./your-project-name
```

Undoubtedly, you have Nuxt.js project on your local computer or github, so copy it now to this directory.

OK, go back to the terminal where you are connected to the droplet and check that files exist in the proper directory:

```shell
ls ./your-project-name
```

You should see a list of the project files.

## Step-Six: Edit LiteSpeed Config File

Open LiteSpeed server configuration file by using this command:

```shell
sudo vi /usr/local/lsws/conf/httpd_config.xml
```

In this file put the following content carefully.

```shell
<extProcessor>
      <type>proxy</type>
      <name>nuxtapp</name>
      <address>127.0.0.1:3000</address>
      <maxConns>100</maxConns>
      <pcKeepAliveTimeout>60</pcKeepAliveTimeout>
      <initTimeout>60</initTimeout>
      <retryTimeout>0</retryTimeout>
      <respBuffer>0</respBuffer>
</extProcessor>

```

## Step-Seven: Create .htaccess File

Create a .htaccess file to your website directory and add Rewrite Rules.

```shell
RewriteEngine On
RewriteRule ^(.*)$ HTTP://nuxtapp/$1 [P]

```

## Step-Eight: Starting Nuxt.js

After successfully followed previous steps let's run Nuxt.js on our server!

```shell
cd ./your-project-name
    npm run build
    npm run start
```

You can see your project by visit your domain or subdomain. Of course, it was great but we need more automatization. Otherwise, you need to start your website from terminal by using previous commands.
***
## Nuxt & PM2: Zero Downtime Deployment

## Getting Started

Make sure you have pm2 installed on your server. If not, simply globally install it from yarn or npm.

```shell
# npm pm2 install
$ npm install pm2 -g
```

## Configure your application

```shell
module.exports = {
  apps: [
    {
      name: 'NuxtAppName',
      exec_mode: 'cluster',
      instances: 'max', // Or a number of instances
      script: './node_modules/nuxt/bin/nuxt.js',
      args: 'start'
    }
  ]
}
```

## Build and serve the app

- Now build your app with ``` npm run build ```.

- And serve it with ```pm2 start```.

- Check the status ```pm2 ls```.

- Your Nuxt.js application is now serving!

