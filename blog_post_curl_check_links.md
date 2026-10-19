# Blog

## Can AI check broken links in your website?
As a technical documentation manager, it is important to ensure that readers can open all the links on your webpages.  Broken links can lead to a poor user experience, and in some cases, can even cause security issues.  When I was a content manager at Intel, I was responsible for maintaining over 700 external links!  It took me some time to develop an automated system for checking and reporting broken links.  This blog post explores how AI may help improve this process.

### AI Capabilities

When asked, Google Gemini confirmed, *"I cannot directly crawl webpages or run automated link-checking tools to test whether hyperlinks are broken or active in real time. I can assist in writing scripts to automate link checking while explaining errors and output from these scripts.  Here's one example using a command line tool called `curl`"*

### What is Curl?

`curl` is a command-line tool capable of retrieving data from a web server.  It can send HTTP requests and retrieve web page content.  To run curl from your MacBook Pro, go to Apps and open Terminal.  Type the command and hit enter.

<img src="images/curl_mac.png" width=500>

`HTTP/2 200` indicates that curl found `https://www.example.com`.   

```bash
curl -L -I http://example.com
```

*  `-L` tells `curl` to follow any redirects
*  `-I` tells `curl` to display the HTTP headers including the status code
*  `http://example.com` is the URL of the website to check for broken links

