---
title: Cypress Testing
description: A simple guide to getting cypress set up.
date: 2021-02-19
layout: layouts/post.njk
tags:
  - testing
---

This week I've started a new job! 🔥

Cypress is a testing tool for your front end web. It doesn't require any
configuration setup to get the 'hello world' of tests up and running.

Check out their [documentation](https://docs.cypress.io/guides/overview/why-cypress.html) for more in depth
explanations to the why and how of cypress.

My simple guide below assumes you have a front end ui with a package.json file
managed with yarn or npm.

Installation
Open your terminal to your project's root folder and enter:

```
npm
npm install cypress --save-dev
```

or

```
yarn
yarn add cypress --dev
```

Then you are going to want to add a few common scripts to your package.json
file.

First we'll add the command that opens the cypress testing window:

// package.json

```json
{
  "scripts": {
    "cypress:open": "cypress open"
  }
}
```

Now you can run npm run cypress:open to open the cypress window.

Write your first test
To get started, in the cypress/integrations folder create a file called
example_test.spec.js. In that file place this simple test that checks if your
app loads:

```js
describe("Login Page", () => {
  it("successfully loads", () => {
    cy.visit("http://localhost:3000");
  });
});
```

Run npm run cypress:open and you'll now see this test listed in the cypress
window.

Automate running your app
One thing is this test assumes to that your app is running at
http://localhost:3000. What we can do is ensure your app is running before
running the test automatically using the start-server-and-test package.

```
npm install start-server-and-test --save-dev
```

or

```
yarn add start-server-and-test --dev
```

Once you've installed that, add the following scripts to your package.json file:

// package.json

```json
{
  "scripts": {
    "start": "command-to-start-your-app",
    "cypress:open": "cypress open",
    "cypress:start-open": "start-server-and-test start http://localhost:3000 cypress:open"
  }
}
```

So what's happening here is the cypress:start-open script runs the
start-server-and-test command. The first argument after that is whichever npm
script you have that starts your application which in this case is, start. Then
it's the url your app will be accessible from, followed by the cypress script we
added earlier.

Go ahead and run npm run cypress:start-open and run your test. Nice to not have
to open another terminal window to run the application.

Run tests in the command line without GUI
This one is simple, whenever you want to run the tests in the command line, say
as a build step on a server, replace cypress:open with cypress:run. No cypress
window will be opening with this, it'll simply run the tests straight away and
display the results in the command line.

Thanks
Thank you for stopping by! If you have suggestions for this post, give me a
shout.
