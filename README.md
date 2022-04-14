**Group:** ​ 2
**Team Members :**
Travis Seevers
David Chan
Brandon Withington
**URL: [http://flip1.engr.oregonstate.edu:42077/](http://flip1.engr.oregonstate.edu:42077/)
Project Report**

**1. Executive Summary:**
    **a.** Summary of Feedback​ **:**
       ● Webpage design was bland and didn’t fit the project theme
       ● Couldn’t click on the battles displayed in the homepage
       ● Some words/pictures were not aligned correctly
       ● Functionality for creating an account/login didn’t work
       ● Newly created battles weren’t displayed on the homepage
       ● Nice layout and navigation design for the project
       ● Some relationships in the table needed to be clarified/modified to
          make it more clear
       ● Not all tables were involved in a query
       ● Didn’t have multi-table queries
       ● Search functionality didn’t work
       ● No validation checks in place
    **b.** Changes Made:
       ● Added validation checks for registering account, creating a battle
          and trying to access the admin page
       ● Changed the color them for the webpage to make it more appealing
          and fitting for the project theme
       ● Added the search functionality
       ● Battles on the homepage navigate to their own individual battles
       ● Newly created battles are also displayed on the homepage
       ● Cleaned up the relationships between tables in our database by
          adding more tables to clarify their relationship and remove
          ambiguity
       ● Included multi-table queries within the project
       ● Added the functionality for registering an account and logging in
          with the registered account
       ● Included all table in some sort of query


```
c. Contribution/Roles:
● Travis:
○ Implemented the initial server infrastructure, search
functionality, login, registration, and account functionality,
and base website infrastructure. As well as contributed to all
reports.
● Brandon:
○ Implemented functionality for adding, inserting and deleting
comments from battles. Worked on CSS and general layout
stylization.
● David:
○ Functionality for adding and deleting admins, starting a
battle, displaying and selecting homepage battles.
Contributed to all of the reports.
```
**2. Project and Database Outlines:**

# Overview

Creature Colosseum is a web application at which users can specify which
particular groups of critters go against another group of critters and vote the victor via a
voting system. Our users can specify both the number and size of the battling critters.
Other users will be able to see the battle and vote on which group would win. Users
would have to create an account to vote and or submit battles to the web application.
This application would seek to entertain people and serve as a time filler.

# Rules & Requirements

**Requirements:**
● Users must log on to interact with the site
○ Interactions:
■ Voting
■ Creating/submitting a battle
■ Creating a comment that appears in the database
■ Deleting comments from Battles
○ Account must have a unique email and screen name, and a secure
password
● Users can search for particular battles
● Each critter in each battle should have a size.


● Users can vote the victor of a battle, which will be stored as a continuous tally of
who is winning currently, with no time frame for the end of the battle.
● Users do not need to log on to see who is winning in a battle, however they
cannot vote if not logged in.
**“Business” Rules :**
● Passwords will be hashed and stored as integers. At no time will a plaintext
password be stored on the servers
● One account gets one vote per battle
● A user can both create battles and comments
● One account can leave as many comments per battle as they wish
● Administrators are identified through their unique screen names, which are
checked when trying to access admin features of the site.
● Each battle must have only 2 critters. The quantity, size, and species fields must
be populated, but the fields don't have to be unique.
● Users can only like or dislike a comment or battle once.
**Entities and Attributes :**

- User: The people who use our web application
    - Email -- This will be unique to the user account, disallowing people to make
       multiple accounts with one email.
    - Screen name -- This will be unique to the user account.
    - Password to log on to the web application -- composed of numbers and letters.
    - Bio -- user’s description that will appear on their profile.
    - User_id -- Unique user identifier
- Critter: A creature that a user will specify to participate in a battle
    - Species -- What does this critter or user look like?
    - Critter_id -- Unique critter identifier.
- Battle: Store the information about the two critter battling, their sizes, quantities, species,
    and respected votes
       - Unique battle identifier to help identify and search for particular battles.
       - Stores the winner between two critters. It keeps track of the vote of both critters.
       - Critter size -- critter size will be categorized as a string value.
       - Critter quantity
          - will be a string value that indicates the number of a particular critter
- Made_by: contains the user id that created the battle
- Comments: Allow the users to voice their opinions on battles. Contains:
- String of the user’s comment
- Likes: Stores the likes of the comment


- Dislikes: Stores the dislikes of the comment
- Comment Id : Unique comment identifier
- Administrator/Moderator: the superusers of the site, have the power to remove admins
and add admins to the sites.
- Admin id: Stores the user id
- Avatar: Image displayed for either a user or a critter. Contains:
- URL of where the image is being hosted
- Text description of what the image is/name
**Potential Relationships (some with attributes):**
● **Takes_part_in:** ​ Must have two critters. Many to many relationship between two critters
and a battle.
● **Votes_for :** ​ many-to-many relationship between the user and battle. Many users vote on
many battles.
● **Can_be** ​: many to one relationship between User and Admin. Not all users are
administrators, but all administrators are users. Only a few are chosen.
● **Comment_of** ​: one-to-many relationship between Battle and Comments.
● **Critter_has_a** ​ : one-to-one relationship between critter and avatar. A Critter must have
an avatar and they can only have one avatar.
**● User_has_a:** ​one-to-one relationship between user and avatar. A User must have an
avatar and they can only have one avatar.
● **Creates_a** ​: one to an optional many. This Describes the relationship between the User
and Battle as a User can create zero or many battles.
**● Comment_of:** ​optional many to optional one relationship between Comments and Battle
since a Battle may have 0 or more comments but a Comment may only be in one Battle.


**3. ER Diagram
4. Schema**


**5. UI Screenshots with Informative Titles and SQL Queries
CREATE/INSERT/ADD NEW Start a Battle Page
"INSERT INTO Battle (Quantity_one, Quantity_two, Size_one, Size_two)
VALUES(?,?,?,?)"
"INSERT INTO Critter (Species) VALUES(?)"
INSERT INTO Takes_part_in (critter_one, critter_two, battle) VALUES(?,?,?)"
"INSERT INTO Critter_has_a (critter, av_id) VALUES (?,?)"
"INSERT INTO Creates_a (battle, usr) VALUES (?,?)"**


**READ/DISPLAY Battles page
"SELECT T.battle as id, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_one) AS Name1, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_two) AS Name2 FROM Takes_part_in T ORDER BY T.id DESC"
"SELECT T.battle as id, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_one) AS Name1, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_two) AS Name2 FROM Takes_part_in T"**


**UPDATE/INSERT/ADD NEW/READ View Battles Page
"SELECT * FROM Comment_of F INNER JOIN Comments C on F.comment_id =
C.comment_id WHERE F.battle = (SELECT battle_id FROM Battle ORDER BY
battle_id DESC LIMIT 1)"
"SELECT B.battle_id, B.Quantity_one, B.Quantity_two, B.Size_one, B.Size_two,
B.votes_one, B.votes_two, (SELECT species FROM Critter C WHERE C.critter_id
= T.critter_one) AS Name1, (SELECT species FROM Critter C WHERE C.critter_id
= T.critter_two) AS Name2 FROM Takes_part_in T, Battle B WHERE T.battle =
(SELECT D.battle_id FROM Battle D ORDER BY D.battle_id DESC LIMIT 1) ORDER
BY B.battle_id DESC LIMIT 1"**


**READ Login Page
"SELECT User_id FROM Usr WHERE screen_name=? AND password=?"**


**INSERT/ADD NEW/CREATE Register Page
"INSERT INTO Usr (screen_name, email, password, bio) VALUES (?,?,?,?)"
"INSERT INTO Avatar (description, image_location) VALUES (?,?)"
"INSERT INTO User_has_a (usr, av_id) VALUES (?,?)"**


**DELETE/READ/INSERT/DISPLAY Admin Page
"SELECT * FROM Usr U WHERE U.User_id NOT IN (SELECT admin_id FROM
Admin )"
"SELECT admin_id FROM Admin WHERE admin_id = ?"
"SELECT * FROM Usr INNER JOIN Admin ON admin_id = User_id"**


**READ/BROWSE/DISPLAY & UPDATE: Account Page
“SELECT screen_name as sc, bio FROM Usr WHERE User_id=?"
"SELECT Avatar.image_location as LNK FROM Avatar JOIN User_has_a ON
User_has_a.av_id=Avatar.av_id WHERE User_has_a.usr=?"
"UPDATE Usr SET bio=? WHERE User_id=?"**


**READ/BROWSE/DISPLAY: View Other Account Page
“SELECT screen_name as sc, bio FROM Usr WHERE User_id=?"
"SELECT Avatar.image_location as LNK FROM Avatar JOIN User_has_a ON
User_has_a.av_id=Avatar.av_id WHERE User_has_a.usr=?"**


**READ/BROWSE/DISPLAY: Search Page (Can search for a user or a battle critter)
"SELECT User_id as id, screen_name as SC FROM Usr"
"SELECT T.battle as id, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_one) AS Name1, (SELECT species FROM Critter C WHERE C.critter_id =
T.critter_two) AS Name2 FROM Takes_part_in T ORDER BY T.id”**


**6. SQL - Triggers/Procedure/Functions/Views**
- Trigger for the table Votes_for:
    - This trigger updates the Battle table depending on the value that was
       inserted into the ‘liked’ column for the Votes_for table. If the value for
       ‘liked’ was 0 then the ‘votes_one’ value for the corresponding ‘battle’ will
       be incremented by 1. Otherwise, if the ‘liked’ value was 1 then the
       ‘votes_two’ value would be incremented by 1 for the corresponding
       ‘battle’.
**Additional Notes:**
Account information for an admin that is already setup in the database/sql code
- Screen name: James
- Password: password
    Account information for a normal user thats already in the database
- Screen name: winghenge
- Password: abcdefg
    Note: more users can be added through the registration page


