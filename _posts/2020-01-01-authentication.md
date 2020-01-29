---
layout: blogpost
title: Authentication 
subtitle: sessionStorage and localStorage in the context of Angular Authentication 
date: 2020-01-01 20:45:23 -0800
main_image: /assets/images/access.jpg
author: Me
categories: [learning]
---
While I was working on my first big Angular web app, the movie database *Movie Admirers* which you can find on this website, I struggled a lot with the **Authentication** part of it. As with many things in programming, once you get the hang of it, it is easy to understand and replicate the concept in other projects. 

## How does authentication work in Angular?
The client sends a request for us to log in. To do this, we enter our data via a form on our Angular app. This is then sent to the server. The server then checks whether we have entered the correct data, i.e. whether username and password match. If it matches, the server sends a *token* back. A token is basically a data packet which is encrypted in a certain way. This token is then stored in our browser, either in a cookie or in the localStorage. With every further request we send (usually one that goes to a sensitive location) we send this token with it. The server can now validate whether the token is valid or not. If the token is correct, the user gets access. However while I was getting my head wrapped around all this, I first had to research the following question:

## What is the difference between sessionStorage and localStorage?
LocalStorage and sessionStorage are integrated in the browser as alternatives to cookies. They store, modify and delete data even if the application is not running online.
This guarantees faster processing and makes it easier to program browser-based applications compared to cookies.
The localStorage is a storage area in the browser introduced with HTML5. In localStorage, the data is stored permanently on the client side i.e. it remains even when the browser is closed. It can only be deleted by the website itself or by the user. However, it should not be forgotten that the client-side storage depends on the system and the browser. If the user uses a different browser or computer, he cannot access the data unless they have also been stored on the server side. SessionStorage, on the other hand, is more short-lived, since it is only bound to the current browser session. Accordingly, the data is deleted as soon as the browser (or even only window/tab, depending on whether the browser sees it as an independent session) is closed.

