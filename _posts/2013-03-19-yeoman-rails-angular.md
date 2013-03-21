---
layout: post
title: Angular + Rails + Yeoman = Angrailman?
category: posts
---

Lots o' new fun tools running around the JavaScript ecosystem right now (Angular, Ember, Backbone, etc...) Only trouble is that the relative immaturity of this space means high costs for new developers trying to navigate the thicket of options for testing, build, workflow, and other development *things*.

I'm not going to wade into the debate around which client side JS framework is the "best". However, for those of you who like AngularJS on the frontend and Rails on the backend, this post is for you. The basic idea is of course to use Rails as the API backend for persistence, session, etc., Under this scenario, it will also serve up the application code as a static asset from the `/public` directory rather than having your frontend code served from a Rails controller or have your assets compiled using the asset pipeline. The reason for this is that I use [Yeoman][yeoman] for client side dependency management, building, testing, and workflow management. I've found the code/review iteration speed is insanely fast with Yeoman's highly polished workflow - add dependencies and make changes while LiveReload pushes all of your changes to the browser in real-time, allowing you to dial in and create some serious focus.

The other thing I like about Yeoman is that is has a large and growing ecosystem of plugins and generators (I use some below), taking the pain out of repetitive tasks and allowing you to focus on building a great user experience.

Here are the basic steps I followed to get this up setup running.

### Prerequisites
* A computer
* Rails
* Node.js
  
### The Setup
1. `rails new myapp && cd myapp`
2. Create a folder where your client-side app will go: `mkdir angular && cd angular`
3. Install Yeoman: `npm install -g yo grunt-cli bower `
4. Neat generators for Angular: `npm install generator-angular generator-testacular`
5. Install all the Yeoman stuff: `npm install && bower install`
    + A couple of caveats for Yeoman:
      + You'll want to install [Grunt-Connect-Proxy][prox] for development. This allows you to proxy HTTP requests to your API to your rails server as you'll be running your app using `grunt server`, part of Yeoman's workflow. You'll probably want to namespace your Rails API behind a `/api` path so that you're not adding each new controller to the proxy whitelist.
      + Change the `dist` folder destination in your `Gruntfile.js` to `../public`. This is where your compiled app assets will be deposited when you `grunt build`
6. Start writing awesome apps.

Yeoman gives you a ton of stuff for free - for instance, you're testing environment will already be configured. The setup I described above, especially when combined with a great frontend framework like Foundation or Bootstrap, has been really productive and fun for me. Hope it helps you!

[yeoman]: http://yeoman.io
[prox]: https://github.com/drewzboto/grunt-connect-proxy
