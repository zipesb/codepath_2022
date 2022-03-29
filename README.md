# Project 8 - Pentesting Live Targets

Time spent: **5** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

login info: pperson StaR!49*whiz

The six possible exploits are:

* Username Enumeration
* ```FOUND``` Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* ```FOUND``` Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* ```FOUND``` Session Hijacking/Fixation

Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.

## Blue

Vulnerability #1: Session Hijacking/Fixation

Description: Blue has a Session Hijacking/Fixation vulnerability. Session Hijacking was specifically tested. If a privileged user signs in to the blue website, they gain access to the staff homepage ```https://<ip-address>/blue/public/staff/index.php```. For the purpose of the exercise the **PHPSESSID** cookie value can be found at ```https://<ip-address>/blue/public/hacktools/change_session_id.php```. If that **PHPSESSID** is given to another user that user can then access the staff homepage without going through the login process, by substituting the stolen **PHPSESSID** for their existing **PHPSESSID** in the cookies of their HTTP requests. This is not possible on the red and green websites because they will change **PHPSESSID** when the **User-Agent** changes.

<img src="blue-vuln1.gif">

Vulnerability #2: __________________

Description:

<img src="blue-vuln2.gif">

## Green

Vulnerability #1: Cross-Site Scripting (XSS)

Description: The green website has an XSS vulnerability in the name and feedback forms of the Contact Us page here ```https://<ip-address>/green/public/contact.php```. Submitting the form with the example XSS code ```<script>alert('Ben found the XSS!');</script>``` in either the name or feedback sections will store the XSS. It will trigger upon an admin visiting the stored feedback at ```https://<ip-address>/green/public/staff/feedback/index.php```.

<img src="green-vuln1.gif">

Vulnerability #2: __________________

Description:

<img src="green-vuln2.gif">


## Red

Vulnerability #1: Insecure Direct Object Reference

Description: The Find a Salesperson page at ```https://<ip-address>/red/public/territories.php``` allows you to click on specific salespeople which brings you to a new page that has a link formatted like ```https://<ip-address>/red/public/salesperson.php?id=1```. The **id** parameter can be iterated through. 1-9 are the **id**s of legitimate sales people viewable by the public. Only on the red site, **id** 10 and 11 are also viewable (e.g. ```https://<ip-address>/red/public/salesperson.php?id=10```) and contain a test "salesperson" and a salesperson that was fired. These two salesperson profiles specifically are not accessible on the blue and green websites.

The two likely causes of this are either improper user authentication on the red website when viewing these two pages (blue and green redirect back to the Find a Salesperson page when trying to view **id**s 10 or 11), or these pages should not be available through the website at all and were mistakenly never removed from the red website.

<img src="red-vuln1.gif">

Vulnerability #2: __________________

Description:

<img src="red-vuln2.gif">


## Notes

Describe any challenges encountered while doing the work

