
Many people create their passwords according to simplicity instead of security. To eliminate this human weakness that often compromises security measures, password policies can be created on all systems that determine how a password should look. This means that the system recognizes whether the password contains capital letters, special characters, and numbers. In addition, most password policies require a minimum length of eight characters in a password, including at least one of the above specifications.


In the previous sections, we guessed very simple passwords, but it becomes much more difficult to adapt this to systems that apply password policies that force the creation of more complex passwords.


This means that many employees often select passwords that can have the company's name in the passwords. A person's preferences and interests also play a significant role. These can be pets, friends, sports, hobbies, and many other elements of life. `OSINT` information gathering can be very helpful for finding out more about a user's preferences and may assist with password guessing. More information about OSINT can be found in the [OSINT: Corporate Recon module](https://academy.hackthebox.com/course/preview/osint-corporate-recon). Commonly, users use the following additions for their password to fit the most common password policies:

|**Description**|**Password Syntax**|
|---|---|
|First letter is uppercase.|`Password`|
|Adding numbers.|`Password123`|
|Adding year.|`Password2022`|
|Adding month.|`Password02`|
|Last character is an exclamation mark.|`Password2022!`|
|Adding special characters.|`P@ssw0rd2022!`|



Considering that many people want to keep their passwords as simple as possible despite password policies, we can create rules for generating weak passwords. Based on statistics provided by [WPengine](https://wpengine.com/resources/passwords-unmasked-infographic/), most password lengths are `not longer` than `ten` characters. So what we can do is to pick specific terms that are at least `five` characters long and seem to be the most familiar to the users, such as the names of their pets, hobbies, preferences, and other interests. If the user chooses a single word (such as the current month), adds the `current year`, followed by a special character, at the end of their password, we would reach the `ten-character` password requirement. Considering that most companies require regular password changes, a user can modify their password by just changing the name of a month or a single number, etc. Let's use a simple example to create a password list with only one entry.


We can use a very powerful tool called [Hashcat](https://hashcat.net/hashcat/) to combine lists of potential names and labels with specific mutation rules to create custom wordlists. To become more familiar with Hashcat and discover the full potential of this tool, we recommend the module [Cracking Passwords with Hashcat](https://academy.hackthebox.com/course/preview/cracking-passwords-with-hashcat). Hashcat uses a specific syntax for defining characters and words and how they can be modified. The complete list of this syntax can be found in the official [documentation](https://hashcat.net/wiki/doku.php?id=rule_based_attack) of Hashcat. However, the ones listed below are enough for us to understand how Hashcat mutates words.

|**Function**|**Description**|
|---|---|
|`:`|Do nothing.|
|`l`|Lowercase all letters.|
|`u`|Uppercase all letters.|
|`c`|Capitalize the first letter and lowercase others.|
|`sXY`|Replace all instances of X with Y.|
|`$!`|Add the exclamation character at the end.|

Each rule is written on a new line which determines how the word should be mutated. If we write the functions shown above into a file and consider the aspects mentioned, this file can then look like this:

#### Hashcat Rule File

Password Mutations

```shell-session
JackTheWizard@htb[/htb]$ cat custom.rule

:
c
so0
c so0
sa@
c sa@
c sa@ so0
$!
$! c
$! so0
$! sa@
$! c so0
$! c sa@
$! so0 sa@
$! c so0 sa@
```

Hashcat will apply the rules of `custom.rule` for each word in `password.list` and store the mutated version in our `mut_password.list` accordingly. Thus, one word will result in fifteen mutated words in this case.

#### Generating Rule-based Wordlist

Password Mutations

```shell-session
JackTheWizard@htb[/htb]$ hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
JackTheWizard@htb[/htb]$ cat mut_password.list

password
Password
passw0rd
Passw0rd
p@ssword
P@ssword
P@ssw0rd
password!
Password!
passw0rd!
p@ssword!
Passw0rd!
P@ssword!
p@ssw0rd!
P@ssw0rd!
```


`Hashcat` and `John` come with pre-built rule lists that we can use for our password generating and cracking purposes. One of the most used rules is `best64.rule`,

#### Hashcat Existing Rules

Password Mutations

```shell-session
JackTheWizard@htb[/htb]$ ls /usr/share/hashcat/rules/

best64.rule                  specific.rule
combinator.rule              T0XlC-insert_00-99_1950-2050_toprules_0_F.rule
d3ad0ne.rule                 T0XlC-insert_space_and_special_0_F.rule
dive.rule                    T0XlC-insert_top_100_passwords_1_G.rule
generated2.rule              T0XlC.rule
generated.rule               T0XlCv1.rule
hybrid                       toggles1.rule
Incisive-leetspeak.rule      toggles2.rule
InsidePro-HashManager.rule   toggles3.rule
InsidePro-PasswordsPro.rule  toggles4.rule
leetspeak.rule               toggles5.rule
oscommerce.rule              unix-ninja-leetspeak.rule
rockyou-30000.rule
```




We can now use another tool called [CeWL](https://github.com/digininja/CeWL) to scan potential words from the company's website and save them in a separate list. We can then combine this list with the desired rules and create a customized password list that has a higher probability of guessing a correct password. We specify some parameters, like the depth to spider (`-d`), the minimum length of the word (`-m`), the storage of the found words in lowercase (`--lowercase`), as well as the file where we want to store the results (`-w`).

#### Generating Wordlists Using CeWL

Password Mutations

```shell-session
JackTheWizard@htb[/htb]$ cewl https://www.inlanefreight.com -d 4 -m 6 --lowercase -w inlane.wordlist
JackTheWizard@htb[/htb]$ wc -l inlane.wordlist

326
```


Create a mutated wordlist using the files in the ZIP file under "Resources" in the top right corner of this section. Use this wordlist to brute force the password for the user "sam". Once successful, log in with SSH and submit the contents of the flag.txt file as your answer.


In order to do this


hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list

* in real world use `best64.rule`* 

 
hydra -l sam -P mut_password.list ssh://10.129.188.219