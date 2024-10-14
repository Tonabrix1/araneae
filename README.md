# araneae (arr-ah-nay)

A multipurpose web-crawler which preforms lightning fast data collection and analysis for application security testing.

araneae can be used to rapidly enumerate a web based attack surface to make finding initial footholds and points of interest simple.

It can also preform a methodical and in-depth analysis in order to find various types of vulnerablities, misconfigurations, and bugs in every inch of an application.

![image](https://github.com/user-attachments/assets/ee840505-9aed-471d-ba7e-bf4f85a458ed)


# What can araneae do?

The basis of araneae is a web crawler, but the actual tool is much more.

Beyond simply collecting endpoints, by default araneae collects response headers, query strings, response timing data, and status codes.

This is where araneae shines, preforming its own static analysis, it can distill this ocean of information into the most interesting drops.

![image](https://github.com/user-attachments/assets/85a87051-c585-4e38-911a-edfb869682dd)

Active analysis can be preformed to elicit interesting responses or automatically find and fuzz parameters for finding myriad vulnerabilities such as xss, sqli, ssrf, and more.
###### *Planned: araneae will dynamically choose scans to preform in steps after collecting data and preforming introspection, such as attacking with xss payloads generated based on content security policies*

![image](https://github.com/user-attachments/assets/2170e838-a620-476b-b68e-60472368a97c)


Further, with araneae's dynamic ![scanner rules](https://github.com/Tonabrix1/araneae/blob/main/rules/README.md) and ![scanner scripts](https://github.com/Tonabrix1/araneae/blob/main/scripts/README.md) users can harness the power of araneae in a few lines of code.

The full help page for the tool is below:

![image](https://github.com/user-attachments/assets/86ff01b8-845f-4daf-a200-a25d1cd446a5)

