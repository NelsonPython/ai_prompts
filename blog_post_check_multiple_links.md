<img src="images/link_rot.png" width=1000 height=200>

# BLOG:  AI Prompt Investigator

## How to Check Multiple Links

[Can AI uncover broken links in your website?](blog_post_curl_check_links.md) introduced using AI Prompts to help automate checking for broken links.  This article follows up with checking multiple links.

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







