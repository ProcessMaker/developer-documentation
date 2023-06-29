---
description: >-
  This guide is meant to help developers to install the ProcessMaker Modeler as
  a standalone application in their local environment
---

# Installing the Modeler

## Overview

In this guide, you will learn how to install and set up the ProcessMaker Modeler, powerful BPMN modeler built on Vue.js and scaffolded using [Vue CLI 3](https://cli.vuejs.org/). This modern and flexible framework provides developers with a solid foundation for creating dynamic and interactive BPMN modeling applications.

## Pre-requisites

{% hint style="warning" %}
Before proceeding with the guide, it's important to assess your skill level as a developer. The following skills and knowledge are highly recommended to ensure a smooth implementation: JavaScript, Web Development Experience, Vue.js, Git Fundamentals, and Command Line Interface (CLI).
{% endhint %}

| Requirement                                                               | Function                                                                                                                                                             | Version        |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| [Node.js](https://nodejs.org/en)                                          | Node.js is a JavaScript runtime environment to run JavaScript on the server-side. It provides the necessary tools and libraries to build and run VueJS applications. | 16.x or higher |
| [Node.js Package Manager](https://nodejs.org/en/download/package-manager) | It is a command-line tool and package manager that comes bundled with Node.js                                                                                        | 8.x or higher  |
| Code Editor                                                               | Choose a code editor of your choice that suits your preferences. Popular code editors for VueJS development include Visual Studio Code, Sublime Text, and Atom.      | Your choice    |

## Modeler Installation Steps

Follow these steps below to set up the [ProcessMaker Modeler](https://github.com/ProcessMaker/modeler/tree/main) and start using it for your project.

### Step 1: Clone the Repository

To install the ProcessMaker Modeler, you first need to clone the repository. Open your terminal and execute the following command:

```sh
git clone https://github.com/ProcessMaker/modeler.git
```

### Step 2: Navigate to the Modeler Directory

Change your working directory to the `modeler` folder by running the following command:

```sh
cd modeler
```

### Step 3: Install Dependencies

To ensure all the necessary dependencies are installed, use NPM (Node Package Manager) by executing the following command:

```sh
npm install
```

### Step 4: Run the Local Development Server

Once the dependencies are installed, you can start the local development server by running the command:

```sh
npm run serve
```

Upon completing the installation and setup process, you should be able to observe the following output/result:

```shell
 App running at:
  - Local:   http://localhost:8081/
  - Network: http://172.25.220.211:8081/
```

### Step 5: Create a Production Build (Optional)

To create a production build of the ProcessMaker Modeler, execute the following command:

```sh
npm run build
```

This command will generate a production-ready build of the application, which can be deployed to a web server for production use.

## Conclusion

The installation process for ProcessMaker's Modeler is simple and can be completed in a few easy steps. By following the instructions provided above, you will be able to successfully install and run the Modeler on your local environment.
