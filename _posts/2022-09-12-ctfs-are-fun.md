---
layout: post
title:  "CTFs are fun"
---


If you are an open-minded person with an interest in IT, I would definitely recommend you to participate in CTF competitions. 
If it's something you haven't heard before, just google it or watch [a video](https://www.youtube.com/watch?v=8ev9ZX9J45A).
Here I'd like to share my thoughts about the topic.

First, I heard about this sort of activity a few years ago when some of my friends shared nice-to-play [Bandit games](https://overthewire.org/wargames/bandit/). There you have to walk through servers, perform some “hacking” and find a password in order to connect to the next level server. No GUI, clear console with SSH connection. It was absolutely fun to do.

It's a great sandbox for practicing in standard UNIX utils like `chmod`, `crontab` etc, but surprisingly I found myself much more interested in web security topics in general. 

Second, some weeks ago while reading the favorite link-aggregator [Lobsters](https://lobste.rs) I found a [post on Garrit Franke's blog](https://garrit.xyz/ctf) with a cool idea to hide a few flags over the blog and call readers to find them. What makes it so nice, is that it's not limited in time like most CTF competitions, and the author also added a "Hall of Fame". Besides that, more hidden flags are to come soon. Well done!

I enjoyed playing over there, so in the following week participated in a few more competitions found on the [CTFtime website](https://ctftime.org/). Good to know, that most of them have sections for all levels of skills, so one should not be a super hacker in order to compete. Funny note: it’s common to find a flag encoded in a so-called “hacker-style” type like `{d0n7_h4cK_m3}` :)

Third, there are also many common topics in that kind of challenge, so any experience you'll gain will be quite useful in the future. 
Few interesting examples over there: 
  * exploiting Flask's template injection (nice article to read [here](https://kleiber.me/blog/2021/10/31/python-flask-jinja2-ssti-example/))
  * exploiting SQL injections (sweet classic)
  * finding hidden API endpoints
  * decrypting cookies
  * digging into robots.txt files
  * extracting credentials from a git history
  ...


This will point any developer and IT-related person to typical pitfalls, one can accidentaly make.
Don't leave holes in your production code!


Happy CTFing!