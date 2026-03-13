# Natas Level X Write-up

## Target
OverTheWire Natas  
Level: X  
Goal: Retrieve the password for the next level.

---

## Reconnaissance
Initial exploration of the webpage was performed.

Observations:
- The page asked for a secret value.
- Incorrect input resulted in the message **"Wrong secret"**.
- This suggested that the application validates the user input against a stored secret.

---

## Source Code Analysis
The page source revealed the following PHP code:

```php
<?
include "includes/secret.inc";

if(array_key_exists("submit", $_POST)) {
    if($secret == $_POST['secret']) {
        print "Access granted.";
    } else {
        print "Wrong secret";
    }
}
?>

Important observations:

The application loads another file using the include statement.

The variable $secret is defined inside includes/secret.inc.

User input from the form is compared with $secret.

Vulnerability

Sensitive information is stored in a file that is directly accessible from the web server.

If such files are not properly protected, attackers can retrieve secrets simply by accessing the file path.

This is known as Information Disclosure.

Exploitation

The included file was accessed directly:

includes/secret.inc

This file contained the secret value used by the application.

After retrieving the secret, it was entered into the input field on the webpage.

The application validated the input and revealed the password for the next level.

Impact

If a web application exposes sensitive files such as configuration files, secrets, or credentials, attackers can bypass authentication mechanisms and gain unauthorized access.

Lessons Learned

Sensitive files should never be accessible from the public web directory.

Secrets should be stored securely outside the web root.

Developers should restrict access to configuration files.

Tools Used

Browser Developer Tools

Manual file path exploration

password is 
**bmg8SvU1LizuWjx3y7xkNERkHxGre0GS**