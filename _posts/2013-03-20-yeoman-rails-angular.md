---
layout: post
title: Angular + Rails + Yeoman = Angrailman?
category: posts
---

Lots o' fun new tools running around the JavaScript ecosystem right now (Angular, Ember, Backbone, etc...) Only trouble is that the relative immaturity of this space means high costs for new developers trying to navigate the thicket of options for testing, build, workflow, and other development *things*.

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
4. Neat generators for Angular: `npm install generator-angular generator-karma`
5. Install all the Yeoman stuff: `npm install && bower install`
    + A couple of caveats for Yeoman:
      + You'll want to install [Grunt-Connect-Proxy][prox] for development. This allows you to proxy HTTP requests from your app to your Rails API as you'll be running your angular app using Yeoman's development server (`grunt server` to start it up). Of course, you will also have your rails development server going to serve API requests. You'll probably want to namespace your Rails API behind an `/api` path so that you're not adding each new controller to the proxy whitelist.
      + Change the `dist` folder destination in your `Gruntfile.js` to `../public`. This is where your compiled app assets will be deposited when you `grunt build`
6. Start writing awesome apps.

As I mentioned above, using Yeoman - as opposed to sticking all of your Angular files into your Rails application structure - has a lot of added benefits: it configures your test environment (Karma), it generates an intuitive, organized folder structure (made all the more powerful by the `generator-angular` plugin I mentioned above), and goodies like LiveReload right out of the box. The setup I described above, especially when combined with a great frontend framework like Foundation or Bootstrap, has been really productive and fun for me. Hope it helps you!

[yeoman]: http://yeoman.io
[prox]: https://github.com/drewzboto/grunt-connect-proxy