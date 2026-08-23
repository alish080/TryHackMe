

Let's dive to isssue, 

Before diving to the website let's understand what is IDOR

## IDOR is a type of access contorl attack vulnerability where attacker can access unauthorized data by manipulating user-supplied input, such as URL or an ID number

---

Now, Start your attackbox and  Lab machine

Once you start the Lab machine that is your vulnerable website we are gonna exploit it,

![ip](/ss/ips.png)

Here in my case, htttp://10.49.165.91 is the vulnerability website

so now open firefox in you attackbox and visit the website,

![login](/ss/login.png)

So, as you can see a login page but we are told if you don't have a account  use guest account 

Let's see view page source or simple press (ctrl+U)

![sourcepage](/ss/source.png)

Here notice the line written in comment, we are told use guest:guest as credentialsas admin is off limit so we type `guest:guest` as a username and password in login page 

![guest](guest.png)

Press login , or Enter

Now you will see a Welcome page , but pay attention to the URL

![vul](/ss/vul.png) 

> profile.php file has a user parameter that refrence using username. The admin elements can be accessed by other users by just changing the `profile.php?user=admin`

SO we will do the same thing 

![found](/ss/final.png)

As , we can see once i changed the user parameter i now can access the  admin page as well and we have our flag

> The Flag : flag{66be95c478473d91a5358f2440c7af1f}

---

## Alish
