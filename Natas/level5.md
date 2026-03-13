# Natas Level 5 Write-up

## Introduction
In this level of OverTheWire Natas, the objective was to understand how web applications handle session information using cookies. This challenge demonstrates the risks of trusting client-side data for authentication or authorization.

## Initial Observation
When the webpage was opened, the site displayed the message:

> Access denied. You are not logged in.

This indicated that the server was checking whether the user was authenticated before granting access.

## Investigation
To analyze the communication between the browser and the server, I used **Burp Suite** to intercept HTTP requests.

### Steps Performed
- Configured the browser to use Burp Suite as a proxy.
- Enabled **Intercept** to capture HTTP requests.
- Accessed the Natas Level 5 page through the Burp browser.
- Observed the HTTP request headers.

While inspecting the request, I noticed the following cookie:
- Cookie: loggedin=0


This suggested that the application was using a cookie to determine whether a user was logged in.

## Analysis
The value `loggedin=0` likely indicated that the user was not authenticated. Since cookies are stored on the client side, they can be modified before the request is sent to the server.

## Experiment
To test whether the server trusted this cookie value, I modified the cookie in the intercepted request:


Cookie: loggedin=1


After forwarding the modified request, the server granted access and revealed the password for the next level.

## Concept Learned
This level demonstrates **insecure client-side authentication**.

The web application relied on a cookie value (`loggedin`) to determine authentication status. Because cookies are controlled by the client, attackers can manipulate them if the server does not properly validate session information.

## Key Takeaways
From this challenge, I learned the following:

- How cookies are used in HTTP requests
- How to intercept and modify requests using Burp Suite
- Why authentication data should not be trusted when stored on the client side
- The risks of insecure session management

## Conclusion
This challenge highlights an important security principle: **servers should not rely on client-controlled data to enforce authentication or authorization**. Sensitive session information should be managed securely on the server side to prevent unauthorized access.

password is **0RoJwHdSKWFTYR5WuiAewauSuNaBXned**