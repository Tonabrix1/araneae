# Scanner Scripts

###### *this functionality is only supported for the default scanning mode that uses grequests, webdriver implementations are planned for the future*

Scanner scripts are scripts that prepare requests to send and return them in a generator object.

To add a scanner script you must simply create a python file containing a function similar to the following:

```py
def endpoints(urls, headers, settings):
    return (grequests.get(url,headers=headers) for url in urls)
```

The `urls` parameter contains the list of urls that the tool is preparing to scan
The `headers` parameter is a dictionary of headers
The `settings` parameter is a dictionary of settings for the tool
The `canaries` parameter is a set of canary strings, which can be used to check for a reflected value in O(1) avg time

This function will return a generator of prepared grequest objects; it's important to use generators (lazy iteration) here to avoid sending the requests when `endpoints` is called.

# Example

Below is an example of a spider script `verbtamperspider.py`:

```py
import grequests
from tools.utilities import add_script_cli_arg

METHODS = ['delete','post','put', 'patch','options','head']

@add_script_cli_arg('verbtamperspider','-vt','--verbtamperspider', help='-vt | (Spider) Fuzzes HTTP request methods in each request\n')
def endpoints(urls, headers, settings, canaries):
    return (getattr(grequests,method)(url,headers=headers) for method in METHODS for url in urls)
```

The `tools.utilities.add_script_cli_arg` decorator can be used to automatically add arguments via `argparse.ArgumentParser.add_argument`.

`action='store_true'` will automatically be passed along with the arguments specified, making the flag a bool which defaults to `False`.

This decorator will automatically activate the script when the flag is used.
