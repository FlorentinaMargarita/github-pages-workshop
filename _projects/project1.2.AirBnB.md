---
layout: project
title: DataMart for Airbnb 
subtitle: Building a database for apartment rentals 
main_image: /assets/images/AIRBNB.png
categories: [PostgreSQL, pgAdmin 4]
---

## Starting the project
 In this project I built a database for storing and processing information regarding the Airbnb use case. I have used Airbnb in the past myself (as a guest, not a host), hence I had the possibility to consult my own Airbnb-profile. 
The first step was to develop an entity relationship model (ERM), which you see in the picture above. To help me design it, I used the app lucidchard. This ER diagram was the basis for developing a database with PostgreSQL.

### Notation Style

At first, I was indecisive between the Chen notation style and the Crow’s Foot/Martin’s style. I ultimately decided for the latter, because of the rather large number of entities we are working with in this project. I feel that the Crow’s Foot Notation gives me a clearer overview, when working with many entities. 

<br>
## Implementing
Implementing the ER-Diagram into a real database, took a lot of effort. Here are the steps I took to achieve it: I chose PostgreSQL as a database system, because I have worked with it before in a different project. To access it, I used pgAdmin 4. Downloading pgAdmin automatically also installed PostgreSQL which was handy. 
I used pgAdmin’s editor to write my SQL-statements. This editor is accessed, by clicking on “QueryTools”. 
Making up and inserting all the dummy data was the longest, yet not the hardest part of the Airbnb DataMart. Instead, coming up with a way to write the Foreign Key Constraints was the most challenging task of this project. 

### Learnings 
The learnings I took away from the project in this step were the following:
<br>

*	Two dashes (--) is how you comment in SQL. 
*	The keyword “UNIQUE” enforces that every entity refers to a different entity.
*	Table names always must be lower case, otherwise you will have to put double quotation marks around them. Which directly leads to the next point:
*	Single quotes and double quotes have a different meaning in PostgreSQL. Single quotes indicate strings. Double quotes are used to denote identifiers. If, for example, I want to start a table name with a capital letter, I will have to wrap it in double quotes. (However, if I start it with a lowercase letter that is not necessary.) On the other hand, if I want to insert a name value, I will do that with single quotes like so: ‘Mary’.
*	After you already implemented the foreign keys, deleting one row will mean, deleting many other rows which are hooked to it by a parent/child relationship.
*	To delete the database completely (which I did for one of my test runs), it was necessary to disconnect the database from the server first, to then be able to delete it. 
*	To make an ER-Diagram in the beginning and thinking the entire process through before jumping right into building the DataMart, was extremely helpful. Thanks to this project I learned to appreciate the advantages of ER-diagrams. Although I found certain flaws which I overlooked in the first draft of the diagram, while implementing the DataMart, it was extremely helpful as a basis of the project. 
*	I learned that with using the “Backup”-function in PGAdmin 4 you can automatically generate an installation file. 
*	This project helped me to better understand the concept of normalization. That, what should be avoided, is to have the same item in a table column by column. I could have probably normalized the data some more, as for example, instead of always using the same entries in “property type”, I could have assigned each property type to a number in a different table and then just writing the corresponding number, instead of writing the property type again and again. That would have saved some storage capacities.
*	I also learned that I can only drop a database when I first disconnect it from the server. Otherwise, it will not work. 


<span class="image"><img src="{{site.baseurl}}/assets/images/psql.png" class="image fit"
                                alt="Main Image" /></span> 

<br>

### MetaData
The data mart can store 20 different entities. The dummy data consists of 20 entries per table/entity. 

<br>

### Here are some funny queries I wrote for my DataMart

--Querying the friendliest host

<span class="image"><img src="{{site.baseurl}}/assets/images/friendliestHost.png" class="image fit"
                                alt="Main Image" /></span> 


--Querying hostnames from worst to best reviewed 

<span class="image"><img src="{{site.baseurl}}/assets/images/hostRank.png" class="image fit"
                                alt="Main Image" /></span> 


--Querying the most expensive place per city for a week, sorted descending 

<span class="image"><img src="{{site.baseurl}}/assets/images/mostExpensive.png" class="image fit"
                                alt="Main Image" /></span> 



--Querying a host in Stockholm who has average_stars rating greater than 3 and a dryer. 

<span class="image"><img src="{{site.baseurl}}/assets/images/hostStockholm.png" class="image fit"
                                alt="Main Image" /></span> 



<br>




###  Here is the Data Dictionary for the initial ERM-Diagram

*Entity: Availability*
AvailabilityId (PK): Int
CalendarId (FK): Int
MinimumNights: Int 
MaximumNights: Int

*Entity: HostAccount*
HostId (PK): Int
HostProfileId (FK): Int
ListingId (FK): Int
Name: String
Email: String
Password: String 
Address: String
Phone: String 
Guest_List: Set
Account_Information: Text
Facebook: String (Explanation: This refers to the link to the Facebook profile.)
Passport_Verification: Boolean 
Total_Listings_Count: Int

*Entity: HealthAndSafety*
HealthSafetyId (PK): Int
ListingId (FK): Int 
Carbon_Mono_Alarm: Boolean
Smoke_Alarm: Boolean
Pets_on_property: Boolean
Security_Deposit: Boolean
Enhanced_Cleaning: Boolean

*Entity: Bookings/Reservations*
ReservationNr (PK): Int
GuestID (FK): Int
BillingNr (FK): Int 
Country_of_Origin: String
Number_of_Nights: Int
HostID: Int
Paid: Boolean 
PaymentPending: Boolean

*Entity: HostProfile*
HostProfileId (PK): Int 
HostId (FK): Int
FeaturesId (FK): Int
HostReviewId (FK): Int
HostName: String
HostSince: Date 
SuperHost: Boolean
ResponseTime: Time
Language: Set
Picture: Varbinary(max)
IdentifyVarified: Boolean
HostAbout: Text

*Entity: Features*
FeaturesId (PK): Int
HostProfileId (FK): Int 
Breakfast_included: Boolean
Host_Identity_Verified: Boolean
HostIsSuperHost: Boolean 

*Entity: Calendar*
CalendarId (PK): Int
ListingId (FK): Int
CalendarLastUpdated: DateTime
CalendarLastscraped: DateTime

*Entity:  Receipts*
BillingNr (PK): Int
ReservationNr (FK): Int
NumerOfNights: Int
TotalPrice: Int
CleainingFee: Int
AirbnbServiceFee: Int
Taxes: Int

*Entity: HostReview*
HostReviewId (PK): Int
HostProfileId (FK): Int
Average_Stars: Int 
Total_Number_Reviews: Int
Explanation for the further attributes of the entity “HostReview” below: 
Cleanliness as well as Communication, CheckIn, Accuracy, Location and Value are rated via five stars which can be either given or not. Because there are five stars, the data type is integer. The attribute “Summary” allows the client to leave a short text with his or her impression of the host.
Cleanliness: Int 
Communication: Int
CheckIn: Int
Accuracy: Int
Location: Int
Value: Int
Summary: Text

*Entity: Amenities* 
AmenitiesId (PK): Int
ListingId (FK): Int
WIFI: Boolean
DishWasher: Boolean
HairDryer: Boolean
TV: Boolean
Washer: Boolean
Dryer: Boolean
Heating: Boolean
Hangers: Boolean
DishWasher: Boolean
Iron: Boolean

*Entity: Property*
ListingId (PK): Int
HostId (FK): Int
CalendarId (FK): Int
AmenitiesId (FK): Int
PropertyPicId (FK): Int
NeighborhoodId (FK): Int
ThingsToKnowId (FK): Int
PropertyType: String
NumberOfGuests: Int
CleaningFee: Int
Price_per_Night: Int
Number_of_Bedrooms: Int
Number_of_Bathrooms: Int
Description: Text
BedType: String
RoomType: String
LocationID (FK) : Int
CheckoutTime: Time
Parking: Boolean
CheckinTime: Time

*Entity: ThingsToKnow*
ThingsToKnowId (PK): Int
HealthSafetyId (FK): Int
CancellationId (FK): Int
HouseRulesId (FK): Int
ListingId (FK): Int

*Entity: GuestAccount*
GuestId (PK): Int
GuestProfileId (FK): Int 
ReservationNr (FK): Int 
Total_Number_Stays: Int
Name: String
Phone: String
Email: String
Password: String 
Address: String
Passport_Verification: Boolean

*Entity: GuestProfile*
GuestProfileId (PK): Int
GuestReviewId (FK): Int 
CountryOfOrigin: String
Picture: Varbinary(max)
Average_Stars: Int
Guest_About: Text
Passport_Verification: Booelan
TotalReviewCount: Int 
GuestSince: Date
Languages: Set

*Entity: GuestReview*
GuestReviewId (PK): Int
GuestProfileId (FK): Int

* Explanation for the further attributes of the entity “GuestReview” below (similar to “HostReview”): 
* Friendliness as well as OverallStars, Cleanliness and Communication are rated via five stars which can be either filled or not. Because there are five stars, the data type is integer. The attribute “Summary” allows the host to leave a short text with his or her impression of the guest.
Friendliness: Int	
OverallStars: Int
Cleanliness: Int
Communication: Int
Summary: Text

*Entity: PropertyImages*
PropertyPicId (PK): Id
ListingId (FK): Id
PictureXL: Varbinary(max)
PictureMedium: Varbinary(max)
ThumbnailPicture: Varbinary(max)

*Entity: Neighborhood*
NeighborhoodId (PK): Int
ListingId (FK): Int 
* Explanation for the further attributes of the entity “Neighborhood” below: 
* Shops and Parks have the data type “Set”, to be able to list all the shops and parks close by.  Safety is a string, so that a short description like “very safe”, “unsafe at night”, etc. can be stored. This would be implemented as a drop-down menu to choose from in the front end. 
Shops: Set
Parks: Set
Safety: String 
Public_Transport: Set
Map: Varbinary(max)

*Entity: Location* 
LocationID (PK): Int
ListingID (FK): Int
District ZipCode: Int
State: Varchar
Country: String
CountryCode: Char
Continent: String
* Explanation for the attribute “Timezone”:
* Timezone has VarChar as its data type, to take in the abbreviation of the time zone e.g., PST, CET, etc. In the implementation the time zone will be automatically stored when the address of the location is saved. 
Timezone: VarChar 

*Entity: HouseRules*
HouseRulesId (PK): Int
ListingId (FK): Int
* Explanation for the further attributes of the entity “HouseRules” below: 
* If the different rules listed below are set to FALSE they will be shown on the user interface next to a red cross to indicate that it is forbidden. If the rule is set to TRUE it will have a green checkmark next to it to indicate that it is allowed. 
Loud_noise_after_11pm: Boolean
Food/drink_in_bedroom: Boolean
Parties_events: Boolean 
Smoking: Boolean
Pets: Boolean


*Entity: CancellationPolicies*
CancellationId (PK): Int
ListingId (FK): Int
Flexible: Boolean
Moderate: Boolean
Strict: Boolean 
Long_Term: Boolean
Super_Strict_30_Days: Boolean
Super_Strict_60_Days: Boolean






