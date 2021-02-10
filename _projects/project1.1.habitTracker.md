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

## Implementation procedure 
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


