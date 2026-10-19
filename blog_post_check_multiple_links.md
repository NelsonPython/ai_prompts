<img src="images/link_rot.png" width=1000 height=200>

# BLOG:  AI Prompt Investigator

## How to Check Multiple Links

In part 1, [Can AI uncover broken links in your website?](blog_post_curl_check_links.md) introduced using AI Prompts to help automate checking for broken links.  This article follows up with AI guidance on checking multiple links.

In my [Portfolio](https://github.com/NelsonPython/publications) there are 212 links.  The following Python function verified 179, but was not able to fully access 33.

```
def check_link_with_curl(url):
    """Runs a curl command to get the exact HTTP status code."""
    error_code = 000
    try:
        result = subprocess.run(
            ["curl", "-s", "-o", "/dev/null", "-w", "%{http_code}", "-L", "--max-time", "10", url],
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True
        )
        status_code = result.stdout.strip()
        
        if result.returncode == 0 and status_code.isdigit():
            return int(status_code)

    except Exception as e:
        print(f'{e}')
        return error_code

curl: The command-line tool used for transferring data to or from a server

-s (Silent): Hides the progress meter and error messages

-o /dev/null: Redirects the downloaded webpage content to /dev/null where it is discarded

-w "%{http_code}": Displays the HTTP status code

-L (Location): If the website responds with a 301 or 302 redirect, curl will automatically follow redirects to the final destination page

--max-time 10: If the server takes longer than 10 seconds to respond, curl will abort the request.
```

### Status 403
When checking the link to a NASA report titled *Toward V&V of neural network based controllers*, the script returned a 403 status.  Gemini suggested the following alternative link.The original URL was located the ACM Digital Library which has strict automated security checkes causing validation scripts to return HTTP 403 Forbidden.  Bypass the access restrictions and retrieve open-access metadata by using the Unpaywall API.

```
#!/bin/bash

echo -e "Toward V&V of neural network based controllers\n"
curl "https://api.unpaywall.org/v2/10.1145/582128.582141?email=Real@email.com"
```

The original URL was located the ACM Digital Library which has strict automated security checks causing automated validation scripts to return HTTP 403 Forbidden.  Bypass the access restrictions and retrieve open-access metadata by using the Unpaywall API.

### Status 405

Another NASA report is available at the Astrophysics Data System (ADS) at Harvard University.  This website is configured so that automated link checkers receive an HTTP 405 Method Not Allowed status.  

```
#!/bin/bash

echo -e "\nPlanning for V&V of the Mars Science Laboratory rover software\n"
curl -I -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" "https://ui.adsabs.harvard.edu/abs/2004aero....1...83F/abstract"
```





