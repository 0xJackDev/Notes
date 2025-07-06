
the CIA triad are the heart of every infosec practitioners role. Without maintaining a balance between them, we cannot ensure the safety and security of our enterprises. We keep this balance by ensuring we audit and account for each file, object, and host in our environment. By validating users have the correct permission to view and utilize those items and ensuring each users identity is valid before granting them access to any enterprise resources. Most breaches can be tied back to losing one of those Three tenets. 

We will focus on Authentication by compromising different user passwords in OS, application and encryption. Lets take a second to discuss auth and its components bit by bit. Before attacking passwords




## Authentication (auth)

Auth at its core is the validation of your identity by presenting a combination of three main factors to a validation mechanism. They are

1. Something you know (aka password)
2. Something you have (id card)
3. Something you are (email address, username, etc)

This process can require any or all of these auth descriptors. These methods will be determines based on the severity of the info or systems accessed and how much they need. For example doctors often require a CAC or a common access car .


## The Use of Passwords

The most common and widely used authentication method is still the use of passwords, but what is a password? A password or passphrase can be generally defined as `a combination of letters, numbers, and symbols in a string for identity validation.` For example, if we work with passwords and take a standard 8-digit password that consists only of upper case letters and numbers, we would get a total of `36⁸` (`208,827,064,576`) different combinations of passwords.


Here are some stats on common passwords used by americans

https://www.pandasecurity.com/en/mediacenter/tips/password-statistics/


https://storage.googleapis.com/gweb-uniblog-publish-prod/documents/PasswordCheckup-HarrisPoll-InfographicFINAL.pdf


The second one by google shows us that 24% of Americans use their children name in a password. or us is the `password re-use` of an already used password for more than one account, `66%`. This means that 66% of all Americans, according to this statistic, have used the same password for multiple platforms. Therefore, once we have obtained or guessed a password, there is a 66% chance that we could use it to authenticate ourselves on other platforms with the user's ID (username or email address). This would, of course, require that we are able to guess the user's user ID, which, in many cases, is not difficult to do.




