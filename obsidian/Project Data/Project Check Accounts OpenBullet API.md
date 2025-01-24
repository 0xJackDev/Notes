

End goal:


I want to make a Website in which a user can enter an email, Full Name, Or any other Personally Identifiable Information (PII) INCLUDING password that could be used to identify them.  This will be locked behind a Membership in which I will Detail pricing and tiers Later. Upon User completing the form and sending out the PII this will go straight into our database, (sql Database will probaly be easiest). I will need a large database of Emails, Passwords, Names and more and need to Organize so each Row in the database is for one person and it includes columns like. First name, Last Name, Password, Emails, . I will need to make this database as large and complex as possible and this will be the majority of the engineering difficultly is acquiring and Sorting data correctly on a mass level. Once they and if they find a row in the Database that matches to the person it will then try all the known email, password combinations to see if any of them are valid. IT WILL ONLY return valid results in the form of JSON. The Backend for Checking these accounts consists of three different actions.

Action 1. 
User Inputs Personally Identifiable Information 

Action 2.
PII is then Matched to a certain row in our database and that row is "Marked"

Action 3.
The marked row Which Has email, password information will then Send this Information to our API of Openbullet
Our API will "check" the email(s)of the marked columns, This Checking consists of using a predetermined list of URLs with open bullet/silver bullet config That Checks if a user account exists on a certain Forum, For example Escape from tarkov you would enter the email into the Forgot Password and it would either say invalid email if no tarkov account or Sent email  if there is.


Action 4.
The api, Without sending the data back to the website will then With any Valid Information, store that in a Valid.txt file and then  Try The Email(s), And Password(s) to any website that has a confirmed account on. 
The backend for this is just also gonna consist of openbullet, except trying to login this time



Action 4:
Return Valid Credentials as well as all other information inside of the row, for example if there is Phone number info also include that. Return this in the form of Json response to the Webpage and Display this to users.


After i do this I can then save all of these VALID credentials i have given into a database of known GOOD credentials. 
