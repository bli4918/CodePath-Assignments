# Project 8 - Pentesting Live Targets

Time spent: 20 hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQL Injection (SQLi)

![Blue - Vulnerability #1 - SQL Injection (SQLi)](https://user-images.githubusercontent.com/58193323/80174218-f9896400-85bf-11ea-929c-77e46c933a7d.gif)

On the Find a Salesperson page, after selecting one of the salesperson’s name, the URL of the page of the information of the salesperson selected ends in “?id=x”, x being a number from 1 to 9. Injecting 'OR1=1' to the end of the URL either redirects you to the previous page you were on, like on the Red and Green websites, or it will display “Database query failed” which indicates an SQLi vulnerability, like on the Blue website.  

Vulnerability #2: Session Hijacking/Fixation

![Blue - Vulnerability #2 - Session Hijacking and Fixation](https://user-images.githubusercontent.com/58193323/80174248-19208c80-85c0-11ea-932b-4a2def92c35f.gif)

Having two different browsers on the Blue website, one logged in as a user and the other not logged in. Then using public/hacktools/change_session_id.php to obtain and change the session id of the one not logged in to the session id of the logged-in user. After refreshing the page of the browser that was not logged in, it should now be logged in as a user due to the change in session id. 

## Green

Vulnerability #1: Username Enumeration

![Green - Vulnerability #1 - Username Enumeration](https://user-images.githubusercontent.com/58193323/80174272-2b022f80-85c0-11ea-9162-fbd621ac7251.gif)

When trying to log in with a correct username, it displays a bolded “Log in was unsuccessful.” while if it was a wrong username, it would display “Log in was unsuccessful.” in plain text. Upon inspecting the page, it is seen that failing to log in with a correct username, the class is “failure” while failing to log in with an incorrect username, the class is “failed”. Unlike the Green website with this vulnerability, the Blue and Red websites always displays a bolded “Log in was unsuccessful.” regardless if the username is correct or not and class is always “failure”.

Vulnerability #2: Cross-Site Scripting (XSS)

![Green - Vulnerability #2 - Cross-Site Scripting (XSS)](https://user-images.githubusercontent.com/58193323/80174294-3a817880-85c0-11ea-8f53-226ba92371b6.gif)

When submitting an entry on the Contact Us page, by entering <script>alert('Bo found the XSS!')</script> in the Feedback section it created an alert when a user is logged in and is going through feedbacks that were submitted. 


## Red

Vulnerability #1: Insecure Direct Object Reference (IDOR)

![Red - Vulnerability #1 - Insecure Direct Object Reference (IDOR)](https://user-images.githubusercontent.com/58193323/80174322-4bca8500-85c0-11ea-9dbd-c0af77e11c56.gif)

On the Find a Salesperson page, after selecting one of the salesperson’s name, the URL of the page of the information of the salesperson selected ends in “?id=x”, x being a number from 1 to 9. On both the Blue and Green website, when the id parameter exceeds 9, it redirects the page back to the Find a Salesperson page while on the Red website, up until id = 11, it displays sensitive information that should not be known to the public.

Vulnerability #2: Cross-Site Request Forgery (CSRF)

![Red - Vulnerability #2 - Cross-Site Request Forgery (CSRF)](https://user-images.githubusercontent.com/58193323/80174332-55ec8380-85c0-11ea-8eb3-d3d5e1149e91.gif)

When logged in as a user and trying to edit an entry in the Salesperson page, if the page is inspected and the initial CSRF token and the entry information is altered then attempting to update the changes would usually redirect to a page that displays “Error: invalid request” like on the Blue and Green website. However, on the Red website, regardless of what the CSRF token is, it will successfully update any changes made to that entry. 

