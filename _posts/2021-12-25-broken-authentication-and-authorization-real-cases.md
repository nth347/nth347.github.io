---
layout: post
title: Broken authentication & authorization - real cases
categories: pentest
---
A few days ago, I have conducted a penetration test for a big customer, surely, they have a complex web application with many functionalities, many roles and privileges. As usual, I went across each endpoint to test for broken authentication & authorization, and yes, I found some flaws in their web application.

## The flaws

Some endpoints do not properly authenticate users, obviously, attackers from the Internet can use the functions on these endpoints without any restrictions. The web application has an endpoint that serves a function that allows sending messages to an arbitrary user on the system, so I've abused it for sending phishing messages to an admin user as proof of concept.

As I know, there are 3 user roles in the application this time, the first role is customers who normally get very few privileges. The next role is low-level admin, users with this role have privileges for managing customers and other small things. After all, the most powerful role is the high-level admin, users belonging to this role can do whatever they want on the system, including managing low-level admins and customers. There is a functionality on the web application that allows a low-level admin to create a customer account and then assign privileges to the new-created account, the interesting thing is that there are no security measures for preventing a low-level admin to assign all available privileges on the system to a customer. What would you do in this situation if you are an attacker with a low-level admin account? But for me, I've created a customer account with my designated username and password, then assigned all privileges to the customer, finally, I've logged in with the customer account, I've become an admin with all powers since then. To make a summary about this flaw, I categorize it as a vertical broken access control that allows privilege escalation.

Additionally, the low-level admin has privilege to renew password of any customer, if the low-level admin clicks `Renew password` button for a customer, an email containing a new password will be sent to the customer's mailbox. Unfortunately, both username and email address can be controlled via request parameters, again, what would you do if you are an attacker with a low-level admin account in your hands? I would click the `Renew password` button for a customer, capture the HTTP request, tamper the `username` parameter to victim username, let's say `victim` (remember, no one prevents me from setting `username` parameter to admin's username), the `email` parameter to my email address, the application going to renew password for `victim` user and send the new password to my mailbox. Thanks to this flaw, I am able to take over any account on the system, including high-level admin accounts if I know usernames.

## Final words

Authentication and authorization are basic security mechanisms in web applications, but sometimes developers can not avoid mistakes when implementing them, sometimes because of a large application, it's not easy to design an efficient authentication & authorization system, and properly enforce it on each endpoint. Don't stop on this, let's find some papers about authentication & authorization and read them. Goodbye!
