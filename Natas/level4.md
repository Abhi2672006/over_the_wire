# Natas Level 4 Write-up

## Introduction
In this level of OverTheWire Natas, the goal was to understand how web servers sometimes rely on HTTP headers to control access. This level demonstrates why trusting client-controlled headers can lead to security weaknesses.

## Initial Observation
When I first opened the webpage, the following message was displayed:

> Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/"

From this message, it was clear that the server was checking the source of the request.

## Investigation
To analyze the request sent by the browser, I used **Burp Suite** as a proxy tool to intercept and inspect HTTP traffic.

### Steps Performed
- Opened Burp Suite and enabled the proxy.
- Used the Burp browser to access the Natas Level 4 page.
- Turned on **Intercept** to capture HTTP requests.
- Observed the request headers.

Initially, the request did not contain a **Referer** header because the page was accessed directly by typing the URL.

After refreshing the page, the request was captured again and the **Referer header** appeared in the request headers.

## Concept Learned
This level demonstrates the use of the **HTTP Referer header**.

The Referer header tells the server from which page the request originated. Some web applications attempt to restrict access by verifying this header.

However, this approach is insecure because HTTP headers are **controlled by the client** and can be modified.

## Key Takeaways
From this challenge, I learned:

- How HTTP request headers work
- The purpose of the **Referer** header
- How to intercept HTTP requests using Burp Suite
- Why client-controlled headers should not be trusted for access control

## Conclusion
This level demonstrates an important web security concept: servers should not rely on client-supplied headers for authentication or authorization decisions. Attackers can manipulate these headers, which may lead to security vulnerabilities.

I got the password **0n35PkggAPm2zbEpOU802c0x0Msn1ToK**

