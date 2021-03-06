---
layout: project
title: Quiz- & Photo-Web-App
subtitle: Quiz and photos for a theatre play
main_image: /assets/images/metropol.jpg
categories: [Angular, Bootstrap, Firebase]
---
Checkout my *theatre-quiz-project in Angular*: <https://quizmetropol.firebaseapp.com/> It was made for a theatre in Vienna, which premiered a new play called "Rock My Soul".  Despite having an English title, the play is in German. Therefore, the entire content of the page is in German as well. 

## A web-app for a new musical
What most developers tell me is that few times you join a new team and start a project from scratch. Instead, you come in and continue the work someone else had started before you (and hope, that it is well documented.) I tried to simulate this by taking the code for a quiz from one of my instructors and changed it into a multiple-choice quiz about a new musical, for a theatre in Vienna. (The story is set in the 70ies, so the quiz tests common knowledge – some of it specific to the play – about that time.) 

## Adding new components
I added a bootstrap photo-carousel feature, for the potential audience to look at stage-photos. I put this photo gallery in a separate component. So, among many other changes, I created another header-component. I did this, because whatever is displayed in the “app.component.html” is always displayed and I now had more than one component. However, since one big change never comes alone, now I also had to implement routing for this SPA. 

## Styling
As I said, the play I made the app for, is set in the 70ies. This is why I used a Google-Font which matches the time: <https://fonts.google.com/specimen/Monoton>
For the Social Icons on the bottom of the page, I used the free icons from FontAwesome <https://fontawesome.com/>


## Hosting on Firebase
Since I wanted to try a new way to launch a page, I hosted it on Firebase, instead of GitHub pages. (Because I previously worked with Google Analytics, GoogleAds and because I use a Gmail-Account daily, I figured that another Google product won't hurt.) I have to say, I was impressed: Firebase works extremely fast and is easy to use!


Creating this app was a lot of fun. Especially, because I notice how much faster I get with each new project.


## Learnings

*	How to implement custom-fonts into an Angular App
*	Hosting on Google Firebase
*	More in-depth understanding of the structure of an angular app.
*	Trying new features in bootstrap like the photo-carousel




