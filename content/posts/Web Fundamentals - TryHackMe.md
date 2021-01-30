+++ 
categories = ["Hugo"] 
date = "2020-08-27" 
description = "Web Fundamentals - TryHackMe Writeup"

featuredalt = "" 
featuredpath = "date" 
linktitle = "" 
title = "Web Fundamentals - TryHackMe Writeup" 
slug = "Web Fundamentals - TryHackMe Writeup" 
type = "post" 
+++


![Web Fundamentals - TryHackMe Writeup](https://miro.medium.com/max/700/0*LomlN9X9qOodvrqj.png)



Welcome to Web Fundamentals TryHackMe Write Up.

## Task 1 - INTRODUCTION AND OBJECTIVES


**NO ANSWER NEEDED**


## Task 2 - HOW DO WE LOAD WEBSITES?

**Things you shoould remember from here.**

```
1. HTTP runs on port 80
2. HTTPS runs on port 443
3. HTTPS uses TLS 1.3
	
4. GET = When we need something from web server.
5. POST = When we send something to web server.
	
Extra : The actual content of the web page is normally a combination of HTML, CSS and JavaScript.
HTML defines the structure of the page, and the content. CSS allows you to change how the page looks 
and make it look fancy. JavaScript is a programming language that runs in the browser and allows you 
to make pages interactive or load extra content.
	
```


**Question 1 : What request verb is used to retrieve page content?**

Hint : When we want soomething from server.

**Question 2 : What port do web servers normally listen on?**

Hint : Normally webservers run on HTTP.

**Question 3 : What's responsible for making websites look fancy ?**
 
Hint : Read Extra carefully. 




## Task 3 - MORE HTTP - VERBS AND REQUESTS FORMATS


**Things you shoould remember from here.**

```
1. For GET requests, a body is allowed but will mostly be ignored by the server.
2. Learn Web Responses it will help you in many cases.

Web Response : https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

```



**Question 1 :  What verb would be used for a login?**
 
Hint : We sending our data to web server.

**Question 2 : What verb would be used to see your bank balance once you're logged in?**
 
Hint : We want our balance from bank web server.

**Question 3 : Does the body of a GET request matter? Yea/Nay**
 
Hint : It's on your remember list of this task.

**Question 4 : What's the status code for "I'm a teapot"?**
 
Hint : Learn Web Responses thorowly.

**Question 5 : What status code will you get if you need to authenticate to access some content, and you're unauthenticated?**
 
Hint : What is the status code of Unauthorized ?




## Task 4 - Cookies, tasty!

**Please Read the task discription you will understad everything from there.**

*No Answer Needed*


## Task 5 - MINI CTF

**Things you shoould remember from here.**

```

1. You can make web requests from your terminal/cmd using *curl*
2. If you use curl *http://tryhackme.com* it will send a GET request by default you can change the request type using *-X POST* remember *-X* is request type changing paramiter.

```

** Task Details **

    GET request. Make a GET request to the web server with path /ctf/get
    POST request. Make a POST request with the body "flag_please" to /ctf/post
    Get a cookie. Make a GET request to /ctf/getcookie and check the cookie the server gives you
    Set a cookie. Set a cookie with name "flagpls" and value "flagpls" in your devtools (or with curl!) and make a GET request to /ctf/sendcookie
    

**Question 1 : What's the GET flag?**

Hint : Send a get request from terminal. Exm:{curl IP:8081/ctf/get}

**Question 2 : What's the POST flag?**

Hint : To get the post flag you have to send a post request with a body. To write a body you need to spacify --data  Exm:{curl -X POST IP:8081/ctf/post --data "flag_please"} 

**Question 3 : What's the "Get a cookie" flag?**

Hint : Go to the URL {IP:8081/ctf/getcookie} and check your cookies. 

```
How to check your cookies ?
Answer : Browser developer tools/Inspect element --> Storeg --> Cookies
```

**Question 4 : What's the "Set a cookie" flag?

Hint : Go to the URL {IP:8081/ctf/sendcookie} go to cookies you will see a + icon there click the icon and create a new cookie name of the cookie will be *flagpls* and value also *flagpls*. After typing press Enter and reload the page. 




## Thanks for reading the Write Up. See You.







