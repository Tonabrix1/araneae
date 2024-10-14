# Scanner Rules

To create scanner rules, you can simply create a python file and insert it into the `rules` directory.

This file must contain a function similar to the one below:

```py
def rule(resp, settings, canaries):
    ...
    return hit
```

The `resp` parameter contains an http response object from the requests module.

The `settings` parameter contains a dictionary with each of the settings for the tool.

The `canaries` parameter contains a set containing all of the canary strings.

This function must return a "hit" object (or None), which is a dictionary in the format:

```py
{   
    'category': category, 
    'url': url, 
    'severity': severity (low/medium/high), 
    'info': description
}
```

# Example

Below is an example from the `reflectedurl.py` rule:

```py
from tools.utilities import Fore, remove_canary, remove_query

local_hits = set()


def rule(resp, settings, canaries):
    if not settings['reflect-endpoints']: return None #early return is optimal

    url = remove_query(resp.request.url)
    url = remove_canary(canaries, url)

    if url in local_hits: return
    local_hits.add(url)

    # since canaries is a set it should generally have an O(1) access time
    if (canary:=resp.request.url.split('/')[-1]) in canaries and canary in resp.text: 
        hit = {
                'category': 'Endpoint Reflection',
                'url': url, 
                'severity': 'low',
                'info': f'{resp.status_code} reflects url canary, possible entry point for XSS and CSP bypass'
            }
        return hit
```