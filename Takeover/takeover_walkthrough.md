![first](cove.png)

Hello let's dive straight to the issue,

---

If you want to see walkthrough video  : https://youtu.be/aWwzMVwBJdE?si=hc9UcuZdnXAPxnP8

---

If you are using Attackbox of TryHackMe then please ignore this part, but if you are using your localmachine then you have do as mentioned below,

> First  you have to connect to the openvpn and configure with the configure file provided by 'Tryhackme access' of your TyHackMe profile.

1. Intsall the openvpn if not installed `sudo apt update && sudo apt install openvpn easy-rsa`

2. once installed check with the command `openvpn --version` if installed you will see the openvpm verison installed in your machine

3. now go to the 'TryHackMe Access' then scroll down, there will be the download option of openvpn configuration file of your profile install it now,

4. Connect it with the configuration file which we downloaded,go to the driver where the configuration is  stored  and run  `sudo openvpn your_configurationfile`

5. Go to TryHackMe Access where you downloaded the configuration file you will see a option "not_connected" turn to  "connected"

> Now we are all set to solve the challange. 

---

Let's look at the task that we are given,

![task](task.png)

If you read task we know that there is a website named Futurevera where space related blogs and reading material and they have been compromised by black hat hacker, the given website link is the root webiste which if you try to open it won't open 

So, we will have to look at other subdomain of the the webiste which might be key to us to look at what's going on

Go ahead and start the machine after 60 seoconds you will be given an ip address of the website 

Once the IP address is given now add that to your `etc/hosts`

> But Why, cause this webiste is virutal hosting meaning one webiste has many services or products so adding the ip and website name we will be able to acess through one ip address ,so for that reason we must do that 

1. Run `sudo nano /etc/hosts`
 
-  Go to the bottom of the file and add the `ip address   futurevera.thm`

For example,

![example](add1.png)

2. Once added try to open it and try with different protocol i.e:`https` or `http` even when you switch protocols there's high chance the website won't open even if it does open it is no use casue  we will have to find other subdomains and see through the SNA through certificate of the website,

3. we will use "fuzzer" they take a massive list of words and try them one by one against a target, we are gonna use fuzzers like

- ffuf (fuzz faster you fool)
- gobuster

> we will use ffuf, to install use `sudo apt install ffuff` just installing this won't be enough you have to install wordlist as well so follow following steps,

- sudo apt update
- sudo apt install seclists -y
 
Now, go where the `seclist` is located usually it is at `cd /usr/share/speclist` so, now it is installed let's find the domain of the website we are given,

4. Open new terminal and Run 

- `ffuf -u https://futurevera.thm/ -H "HOST: FUZZ.futurevera.thm" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 0`

so as you run this you will see subdomains that are open for this website (Here might me `portol` and `payroll` )

you will 2 subdomains open so we will add to our `/etc/hosts` so we can access the website

Now go to `sudo nano /etc/hosts` and add `portol.futurevera.thm` and `payroll.futurevera.thm`

![adding subdomains](add2.png)

5. Now go to the webiste check <https://portol.futurevera.thm> and <https://payroll.futurevera.thm>

the website is open but doesn't seem much of a help so we will see its certificate if we can get which will be help or hint to us ; go to lock icon located at the side of search bar and go to the security option and see certificates

![certificate](cert1.png)

if you scroll down you won't see much usefull things so, Search for another subdonmain using our `ffuf` command we used earlier 

> You won't find another subdomains so now we will use social engineering ,we know that there is 'blog' page casue CEO has mentioned that they used to post blog and were building <support> so there must be  `blog and support page` let's try that

6.Let's add `blog` and `support` subdomains to our `etc/hosts`

![adding_another_sub](add3.png)

now let's go to our blog page and see if we have some things that will be helpful and same for the support page

Looks like there is nothing in blog certificate too, let's see support page

If you see `https://support..futurevera.thm` and go to see its certificate and scroll down you will see a alternative name SAN (subdomain alternative name) if you search that name with `https` or `http`

- http://SAN-you_will_find
OR,
- https://SAN-you_will_find

and if you look at search box you will see a flag remove the uncesssary things and paste the flag,

![flag](final.png)

---
***Alish***

