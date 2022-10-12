---
layout: post
title:  "Hide annoying modals with Demodal"
---

Contemporary web pages are very annoying. (Almost) any random website visiting flow starts from 
 * clicking on the cookie policy popup
 * clicking on the 'subscribe for our super exciting news' popup
 * clicking on the 'please disable Adblock' popup
 * clicking on the 'download our app' popup
 * clicking on the 'super deal just for you and only now' popup

Then, finally, the awesome content you were looking for is readable.


And there’s even more fun for you, if the browser hasn’t stored cookies since the last visit, or you wiped them, or you used an 'incognito' mode, you’ll have to repeat these steps next time.

In short words, web is a way more aggressive environment now.

Adblock-like solutions or personal DNS servers like Pi-Hole are definitely great tools, but they serve slightly different purposes: filter all the ads and crap from pages. Cookie consent often makes a page unavailable to read until you click a button over there. For example, Google’s consent popup covers all the page. 

![Google page](/assets/images/google-cookie-screen.png){: width="600"}


There's an excellent tool that I found useful [Demodal](https://github.com/AliasIO/demodal). It follows the Unix philosophy and does simple things: clicks buttons or removes annoying parts of web pages right after they appear.

Anyone familiar with the basics of HTML will create a config easily. Here's an example of config for clicking an element with class `.cookieOverlayBtn` in any subdomain of Estonian state news agency [err.ee](https://www.err.ee) 

![Demodal window](/assets/images/demodal-window.jpg){: width="600"}


Pretty easy, nah?

I personally prefer to automatically wipe all the cookies from sites like this one, so clicking dumb consent is an extremely useful feature for me. 

Also, there is one more very nice tool, which can serve the same purpose: [Greesemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/). It works in a more generic way: runs custom JS pieces, so potentially can be used for more advanced automation. I advise taking a look at it as well.

Happy browsing!