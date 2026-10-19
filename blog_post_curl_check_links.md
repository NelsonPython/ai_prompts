# Blog

## Can AI check broken links in your website?
As a technical documentation manager, ensuring that readers can easily navigate your content is important.  Broken links can frustrate users, degrade the overall user experience and, in some cases, even introduce security or compliance issues.  

When I was a content manager at Intel® I was responsible for maintaining over 700 external links!  It took me some time to develop an automated system for checking and reporting broken links.  This blog post explores how AI may help improve this process.

### The Reality of AI Capabilities

When asked, Google Gemini confirmed, *"I cannot directly crawl webpages or run automated link-checking tools to test whether hyperlinks are broken or active in real time. I can assist in writing scripts to automate link checking while explaining errors and output from these scripts.  Here's one example using a command line tool called `curl`"*

### Harnessing `curl` for Link Checks

`curl` is a command-line tool capable of retrieving data from a web server.  It can send HTTP requests and retrieve web page content.  

`HTTP/2 200` indicates that curl found `https://www.example.com`.   

```bash
curl -L -I http://example.com
```

*  `-L` tells `curl` to follow any redirects
*  `-I` tells `curl` to display the HTTP headers including the status code
*  `http://example.com` is the URL of the website to check for broken links

### Take a Test Drive

To run curl from your MacBook Pro, open Finder, go to Apps, and open a Terminal window.  Enter the curl command and press enter.

<img src="images/curl_mac.png" width=500>

### Automating `curl`


