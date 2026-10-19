<img src="images/link_rot.png" width=1000 height=200>

# BLOG:  AI Prompt Investigator

## How to Check Multiple Links

Part 1, [Can AI uncover broken links in your website?](blog_post_curl_check_links.md) introduced using AI Prompts to help automate checking for broken links.  This article follows up with AI guidance on understanding HTTP status codes.

In my [Portfolio](https://github.com/NelsonPython/publications) there are 212 links.  The following Python function is part of a script that verified 179 links, but was not able to fully access 33 links.  Some link checks resulted in HTTP 403 and others in HTTP 405.

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
```

curl: The command-line tool used for transferring data to or from a server

-s (Silent): Hides the progress meter and error messages

-o /dev/null: Redirects the downloaded webpage content to /dev/null where it is discarded

-w "%{http_code}": Displays the HTTP status code

-L (Location): If the website responds with a 301 or 302 redirect, curl will automatically follow redirects to the final destination page

--max-time 10: If the server takes longer than 10 seconds to respond, curl will abort the request.

---

## Alternative Methods

When asked, Gemini recommended alternative methods for link checks with status 403 and 405.

### Status 403

When checking the link to a NASA report I wrote, titled *Toward V&V of neural network based controllers*, the script returned a 403 status.  The original URL is part of the ACM Digital Library which has strict automated security checks causing validation scripts to return HTTP 403 Forbidden.  According to [RFC 9110: STD 97: HTTP Semantics](https://www.rfc-editor.org/info/rfc9110/#section-15.5.4), the 403 (Forbidden) status code indicates that the server understood the request but refuses to fulfill it.  Status code 403 indicates that the link is not broken.  That may be sufficient evidence.  Gemini suggested trying an alternative, the Unpaywall API to retrieve open-access metadata.

```
$ curl "https://api.unpaywall.org/v2/10.1145/582128.582141?email=Real@email.com"

{"best_oa_location":null,"data_standard":2,"doi":"10.1145/582128.582141","doi_url":"https://doi.org/10.1145/582128.582141","first_oa_location":null,"genre":"proceedings-article","has_repository_copy":false,"is_oa":false,"is_paratext":false,"journal_is_in_doaj":false,"journal_is_oa":false,"journal_issn_l":null,"journal_issns":null,"journal_name":"Proceedings of the first workshop on Self-healing systems","oa_locations":[],"oa_locations_embargoed":[],"oa_status":"closed","published_date":"2002-11-18","publisher":"ACM","title":"Toward V&V of neural network based controllers","updated":"2026-08-21T15:25:14Z","year":2002,"z_authors":[{"author_position":"first","is_corresponding":false,"raw_affiliation_strings":["RIACS/NASA Ames"],"raw_author_name":"Johann Schumann"},{"author_position":"last","is_corresponding":false,"raw_affiliation_strings":["Nelson Consulting Company"],"raw_author_name":"Stacy Nelson"}]}
```

While the output is very technical, I can see the name of the report and my name as raw_author_name.  This is evidence that the link is not broken.


### Status 405

Another NASA report is available at the Astrophysics Data System (ADS) at Harvard University.  This website is configured so that automated link checkers receive an HTTP 405 Method Not Allowed status.  [RFC 9110: STD 97: HTTP Semantics](https://www.rfc-editor.org/info/rfc9110/#section-15.5.6) Paragraph 15.5.6 says *In plain English, a 405 Method Not Allowed error means that the server understood what you were trying to do, but it doesn't allow you to do it that way on that specific page or web address.*  Status code 405 presents strong evidence that the link is not broken.  Gemini recommended a `curl` command to fetch only the HTTP headers.

```
$ echo -e "\nPlanning for V&V of the Mars Science Laboratory rover software\n"
curl -I -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" "https://ui.adsabs.harvard.edu/abs/2004aero....1...83F/abstract"

Planning for V&V of the Mars Science Laboratory rover software

HTTP/2 405 
server: awselb/2.0
date: Mon, 19 Oct 2026 23:44:46 GMT
content-length: 2203
x-amzn-waf-action: captcha
cache-control: no-store, max-age=0
content-type: text/html; charset=UTF-8
access-control-allow-origin: *
access-control-max-age: 86400
access-control-allow-methods: OPTIONS,GET,POST
access-control-expose-headers: x-amzn-waf-action
```
This evidence is less clear but it indicates that the server returned a 2203-byte body.  This is typically an HTML page containing the CAPTCHA challenge interface or an error message.  The response payload is formatted as an HTML document rather than raw data or JSON. OPTIONS,GET, and POST have been explicitly defined as the allowed request types. Notice that HEAD is absent, which directly corroborates the 405 Method Not Allowed status.

---

 **References**

IANA Internet Assigned Numbers Authority [Hypertext Transfer Protocol (HTTP) Status Code Registry](https://www.rfc-editor.org/info/rfc9110/#section-15.5.6)







