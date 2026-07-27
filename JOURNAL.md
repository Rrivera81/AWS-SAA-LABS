## Day 1 Recap - July 24, 2026
Today I just created a AWS free tier account. I had to set up the MFA, Billing and the IAM creating a Admin user as well, 
at first I had truoble on where to locate all the right channels, 
but after some time I figured it out. 
Once creating the account and setting everything up properly when it came time to log in I didin't know my account ID so there was alot of back and forth trying to find the proper info. 
But once I found everything is set up properly for Day 2 and on.

-------------------------------------------------------------------------------------------------------------------------------
## Day 2 — July 25, 2026
First custom IAM policy by hand. Proved explicit deny beats allow.
Hit a JSON syntax error adding the second statement — each statement
needs its own braces + comma. EC2 role test: no creds = fail, attach
role = works. Core Four rep 1 (IAM): 2:01.41

-------------------------------------------------------------------------------------------------------------------------------
## Day 3 — July 26, 2026
EC2 Fundamentals lab. Launched t3.micro with user data (Apache),
served a page, tested security group by breaking/fixing the HTTP rule.
Core Four IAM rep 2: 1:03.80 (down from 2:01.41). Instance terminated.
