---
description: >-
  This guide discusses how to install ProcessMaker's Screen Builder as a
  standalone application.
---

# Installing the Screen Builder Standalone Application

## Overview

In this guide, learn how to install and set up ProcessMaker's Screen Builder, a powerful [VueJS-based](https://vuejs.org/) tool for creating dynamic digital forms called "Screens" in ProcessMaker Platform.

## Prerequisites

{% hint style="warning" %}
Before proceeding with the guide, it's important to assess your skill level as a developer. The following skills and knowledge are highly recommended to ensure a smooth implementation: JavaScript, Web Development Experience, Vue.js, Git Fundamentals, and Command Line Interface (CLI).
{% endhint %}

| Requirement                                                               | Function                                                                                                                                                             | Version        |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| [Node.js](https://nodejs.org/en)                                          | Node.js is a JavaScript runtime environment to run JavaScript on the server-side. It provides the necessary tools and libraries to build and run VueJS applications. | 16.x or higher |
| [Node.js Package Manager](https://nodejs.org/en/download/package-manager) | It is a command-line tool and package manager that comes bundled with Node.js                                                                                        | 8.x or higher  |
| Code Editor                                                               | Choose a code editor of your choice that suits your preferences. Popular code editors for VueJS development include Visual Studio Code, Sublime Text, and Atom.      | Your choice    |

## Screen Builder Installation Steps

Follow these steps below to set up the [ProcessMaker Screen Builder](https://github.com/ProcessMaker/screen-builder) and start using it for your project.

### Step 1: Clone the Repository

To install ProcessMaker Screen Builder, clone the repository. Open your terminal and execute the following command:

```sh
git clone https://github.com/ProcessMaker/screen-builder.git
```

### Step 2: Navigate to the Screen Builder Directory

Change your working directory to the `screen-builder` folder by running the following command:

```sh
cd screen-builder
```

### Step 3: Install Dependencies

To ensure all the necessary dependencies are installed, use NPM (Node Package Manager) by executing the following command:

```sh
npm install
```

### Step 4: Run the Local Development Server

After the dependencies are installed, start the local development server by running the command:

```sh
npm run serve
```

Upon completing the installation and setup process, you should be able to observe the following output/result:

```shell
App running at:
  - Local:   http://localhost:8080/
  - Network: http://172.25.220.211:8080/
```

### Step 5: Create a Production Build (Optional)

To create a production build of the Screen Builder, execute the following command:

```sh
npm run build
```

## Conclusion

The installation process for ProcessMaker's Screen Builder is straightforward and requires a few simple steps. By following the provided instructions, developers can set up ProcessMaker's Screen Builder in their development environment and be ready to create and customize dynamic digital forms.
