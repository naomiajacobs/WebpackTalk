# WebpackTalk
Slides from my talk, Webpack: It's Not Magic.

Transcript to come.

Visit the page for this at https://naomiajacobs.github.io/WebpackTalk.

## Transcript (lightly edited)
### One paragraph per slide, stars * at transitions within slides

Hi, my name is Naomi. I'm a software engineer at Mavenlink, we're a software company in San Francisco, and we make project management software for consulting firms. We have a pretty cool culture, we do pair programming, and yes, we are hiring! If you're interested, please come up and talk to me afterward. Currently, on my team I'm helping to transition away from Backbone by building our first feature in React. But today I'm here to talk to you about Webpack! Let's get started.

Why are we talking about Webpack today? Well, it's a tool for web developers that is * one: very popular, and 2: not well-explained, as far as I can tell.

How popular? This data is from npm, the JS package manager, and it's tracking downloads per week for Webpack and some similar tools, Gulp, and Grunt, and Browserify. Webpack is the red line, and we're tracking from 2014 to 2017. So as you can see, Webpack has gotten pretty popular. And if you're wondering what that giant dip is all the way at the end, that's the winter holidays, nobody codes on the holidays. The first stable version of Webpack was released in January of 2014, and as you can see, since then it's gotten more and more popular, and now it has over a million downloads per week. That means that there are a lot of people using Webpack, and as far as I know, a lot of people who are confused about how to use Webpack, so have any of you used Webpack before? Awesome! Cool, I'm glad to see that.

So, how did I learn Webpack? I used it for a couple of side projects, cause I wanted to use React, and when I learned it, I thought that its documentation and API were really confusing. It felt like pretty much all I was doing was copy-pasting from Stack Overflow into my config file until things worked, and I had no idea why. Have any of you guys done the same thing? Yeah, ok, good, I'm glad. I thought it was really confusing, and I sort of put it away, and I was like "Wow, it's cool, it seems like it can do a lot of things, but I'm gonna forget about it for now." * But then my company, Mavenlink, started using Webpack to compile its assets when we did the switch from Backbone to React, and suddenly I *had* to figure out what was going on, and I realized that learning how to use a tool is a lot harder when you don't know how it works. So I started trying to figure out, you know, what Webpack was doing under the hood, and I found a ton of stuff on how to set up my config file, but not really very much about what it was actually doing. So, I started doing some research, and today I want to share with you what I've learned. * I want to do this because I think that we're all better and happier developers when we understand our tools, so the idea here is going to be to demystify what Webpack is doing when it creates an asset, cause that's going to make it easier for you to understand what's going on when you're debugging through a Webpack asset, or trying to figure out why a build failed, and it's going to lay the foundation for being able to understand all of the fancy things Webpack can do.

So today, we're going three questions: What is Webpack? What problems does Webpack solve, and How does it work? Let's start with what it is.

So, as Webpack describes itself, it is a module bundler that takes modules with dependencies and emits static assets representing those modules. When I first heard that I had no idea what any of that meant, so the way that I like to think of it is that Webpack takes stuff that is nice for you to write and turns it into stuff that is nice for your browser to read. Let's talk about what that means.

So, easy for you to write means that it's easy for humans to read and write. We have pretty formatting, we have readable variable names, our code is separated into multiple files so that we can separate it logically. It might not even be in a language that the browser can understand. ES6, also known as ES2015, is the new specification for JS, but browsers haven't implemented a lot of the new features yet. Some people don't even want to write in JS, they want to use a language that transpiles to JS, like CoffeeScript, or TypeScript, or Clojurescript. * But what's nice for your browser to read is old-school JS, right? ES5, the standard stuff. We want to make fewer requests, which is great for bad internet connections, and we want to have smaller responses, right? We don't need whitespace or pretty variable names, the browsers don't care about that, only we do. And, as you'll be able to see, Webpack is going to help us do those transformations.

What problems does Webpack solve?
