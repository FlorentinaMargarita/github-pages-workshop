---
layout: project
title: Habit Tracker
subtitle: Tracking App in Django.  
main_image: /assets/images/habitTracker.PNG
categories: [Django, Python, SQLite]
---
Check out the *Habit Tracker* here: <https://habit-tracker-by-florentina.herokuapp.com/>

*Habit Tracker* was my first project written in Django. 

## The Design

On the front end the habit tracker lets you generate new habits by clicking on the “Make New Habit” button on the upper left of the interface. 
Once you click it you are forwarded to the page where you can create a new habit. The left field is for the new habit name and in the right field you can decide the habit’s interval: Either daily or weekly. 

Depending on the interval you chose, the habit will then be displayed on two lists: The top list “All Habits”, where all habits are tracked. As well as on one of the bottom lists of the respective time interval, namely “Daily Habits” or “Weekly Habits”.

The rows in the “All Habits” section provide following metrics for each habit:

* “Repeated so far”: This indicates how often the habit was repeated in total.

* “Current Streak”: This shows the streak the user is currently in. If, for example, it is a weekly habit, it shows how many weeks – counting from the current week backwards – the user has checked the habit. 

* “Longest Streak”: This is the longest streak of this habit of all time. This can either be the current streak, or some other streak that has since been interrupted, but is longer than the current streak.  

Furthermore, the rows in the “All Habits” section provide buttons to allow the user to check, update, delete and view the respective habit. 
The user should press the button “check” if he/she repeated the habit that day.

* When updated, the user gets the chance to change the name and interval of the habit. The streaks-count will remain the same. 

* When deleted, the entire habit disappears entirely. 

* When the user clicks on the “View” button he or she will be forwarded to the analytics-section of this specific habit. Note: This is not the analytics section of all habits. Just this specific one. 



<span class="image"><img src="{{site.baseurl}}/assets/images/habitTracker_new.PNG" class="image fit"
                                alt="Habit Tracker" /></span> 

## The aim of this project

The aim of this project was to build a habit tracking app in Python. The focus lay especially on the backend and the use of an object-oriented programming style as well a functional programming style. Although I had a good understanding of object-oriented programming, I still had to get acquainted with the concepts of functional programming. When doing the research, I understood that functional programming is built on pure functions. Pure functions have no side effects. They are completely self-contained, and they do not affect any variables outside of them. With pure functions you will always get the same output for the same input. For me, the most important aspect to understand functional programming was the insight that pure functions never read from or write to the database. 
For this project I decided to work with a Python framework called Django. Due to the frontend capabilities of Django, the required analytics part of the project is visualized on the user interface. The first step to learn it was to read Django documentation and articles on the internet as well as to follow a couple of different YouTube-tutorials. 

## Technical summary

The example tracking data which can be used to run the tests in the project are stored in a json file called “data fixtures”. This data can be used twofold: On one hand the data fixtures can be used to populate the database (SQLite3) which comes out of the box with Django. (This was very handy during development, because I could test different functions on the example data, without manually having to rewrite them to the database.) On the other hand, the data fixtures are used for testing as follows: In the test file the data is loaded into a database, on which you can run the tests. However, once the tests are run and results are obtained this testing-database will be automatically deleted, but more on this later.

There are two main classes in this project: Repeats and Orders. The latter represents the habits. The time, whenever a habit is completed or – as I call it in the code – “checked” a “Repeats”-object is stored as a charfield in the database. All the further attributes which the habit tracker tracks (current streak, longest streak, interval) pertain to the Order class. So, whenever a habit is “checked” a “Repeats”-Object is generated and referenced to via a many-to-many-field called “checkedList” in the Order object. 

All those aspects mentioned so far were relatively easy to implement. The part which took most time and effort was to create a function that counts the current and the longest streak. I came up with a solution with an imperative paradigm rather quickly (with a lot of nested for-loops etc.) However, the aim of this project was to build a significant part of the logic using the functional programming paradigm. As mentioned above, code written in a functional programming style primarily uses functions without side effects. The calculation of streaks (longest streak and current streak) in the function ‘getStreak()’ is written in functional programming style. The functions inCheckedDays(), tryingDaily() and tryingWeekly(), inside the function getStreak() are pure functions, which means that they have no side effects. I used Python’s itertool “accumulate” to calculate the current and longest streaks.  To compute current streak and longest streak simultaneously I decided to use the Python data type called “tuple” (current streak being the first, longest string being the second value of the tuple.)

Object-oriented programming uses groups of methods and fields called objects. I used the Object-oriented programming style to help with streak testing. Therefore, I wrote a class in the test-file called StreakTester(). The methods I used are streak_printer(self), which calculates the streaks and prints information about the result and change_order(self, habit), which updates the habit (order) on the instance in order not to have to make a new instance of StreakTester every time.  

To implement the habit tracker and to calculate streaks, I had to define what a day is, and what a week is. I will give examples for each, as this is probably the best way to describe the usage of them. This habit tracker defines a day, starting as of yesterday. Here is an example: Suppose today is Wednesday and the last time you did the habit was Monday. Then the current streak is 0 and the longest streak is one. Suppose today is Wednesday and the last time you did the habit was Monday and Tuesday. Then the current streak is two and the longest streak is two as well. Suppose today is Wednesday and the last times you did the habit was Monday, Tuesday and today. Then the current streak is still 2 and the longest streak is still 2 as well (today is ignored and will be only calculated tomorrow). The reason for this is, that if I would count today also, the app would show the current streak at 0 even if it has only been a few hours into the new day (today). 

Now that I have explained how this project deals with days, I will now explain how it works with weeks and how it defines them. Again, I will illustrate it, using an example: Suppose today is Wednesday. The first week which the code looks at is from last Wednesday to this Tuesday. The week starting today is not being looked at. Hence the definition of a start of the week, is whatever today is. 
Once everything was up and running, I wrote the unit tests. Django uses its own testing framework.  It will run all the tests which are in the tests.py file. To do that, Django is creating a test-SQLite database. Django puts this testing database in memory, runs all tests and once they are completed, destroys this database out of memory. 


## Implementation procedure in more detail
#### The function “home”:

* For each habit, the program computes how often it was checked
* It filters the habits for the two intervals (weekly, daily) to be able to then 	display them separately. 
* It is used on the landing page (“Home” tab).

<br>
#### The function “analytics”: 

* It computes the number of habits tracked. 
* It finds the habit with the longest streak. 
* It finds the habit with the most checks in total. 
* It is used on the analytics page (“Analytics” tab).

<br>
#### The function “habit”: 

* Checks the following metrics for a specific habit: when it was created, how often it was repeated, the current streak and the longest streak. 
* It lists all the instances (“Repeats”) when this specific habit was 	checked. 
* It is used on the analytics page for a specific habit. (You get to it by 	clicking the “View”- button next to a specific habit.)

<br>
#### The functions “createHabit”, “updateHabit” and “delete”: 

* “createHabit” saves a new habit to the database. 
* “updateHabit” overwrites an existing habit with new information.
* “delete” deletes a specific habit from the database.
* Those three functions are used by the form page, which is accessed 	either by clicking 	“update”, “delete”, or “make newhabit” on the home-tab.

<br>
#### The function “checkhabitfaketoday”: 

* Whenever a habit is checked, it creates a new instance of "Repeats", which stores the dateTime as a string in the database. 
* The habit which was checked, references this Repeats-object in a 	ManyToManyField. 


<br>
#### The function “getStreaks”: 

* The “getStreaks” function is the heart of the code. It has several functions within it. (e.g., to determine the range of a week).
* In broad brush strokes it can be said that “getStreaks” computes the longest streak as well as the current streak, by comparing the checked days to all the days since the first check was ever done. 

* “getStreaks” receives two arguments: “order” and “today”. “order” stands for the habit-object. “today” stands for the day, we are counting backwards from. This is done, to then compute whether we are in a streak or not and if, how long this current streak is and if it is a new “longestStreak”. In the user interface version, “today” will always be the date of today. This is done by using a different function on top called “checkHabitFakeToday”, which will only be called if you press the button on the user interface. However, if you test the code in tests.py, today will be set to the fixed date, in order to get meaningful results without having to press the button on the user interface.





<span class="image"><img src="{{site.baseurl}}/assets/images/habitTrackerLogo.PNG" class="image fit"
                                alt="Main Image" /></span> 


## Going forward
At this point only one user can utilize the habit tracker.
It is a future project of mine to implement user authentication together with the possibility to create a user account, to allow multiple users to use the app simultaneously. 



<span class="image"><img src="{{site.baseurl}}/assets/images/habitTracker_analytics.PNG" class="image fit"
                                alt="Main Image" /></span> 


