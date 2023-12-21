# Cross-Site Request Forgery (CSRF) Attack Report

## Overview

Cross-Site Request Forgery (CSRF), also known as XSRF, Sea Surf, or Session Riding, is a type of malicious exploit of a website where unauthorized commands are transmitted from a user that the web application trusts.

## How CSRF Works

A CSRF attack specifically targets state-changing requests, not theft of data, since the attacker has no way to see the response to the forged request. The attack works by including malicious code or a link in a page that accesses a web application that the user is believed to have authenticated. If the user is authenticated, the application trusts the user and the attacker's malicious script.

## Example of CSRF Attack

1. A user logs into `www.example.com`, using forms authentication.
2. The server authenticates the user and issues a response that includes an authentication cookie.
3. The user visits a malicious site.
4. The malicious site contains an HTML form similar to this:

   ```html
   <form action="http://www.example.com/transfer" method="POST">
     <input type="hidden" name="amount" value="1000"/>
     <input type="hidden" name="account" value="attacker"/>
   </form>
   <script> document.forms[0].submit(); </script>
This form is automatically submitted by the JavaScript `document.forms[0].submit();`, and the user unknowingly makes a transfer to the attacker's account.

## Prevention Techniques

### Use Anti-CSRF Tokens
A random token that is unique for each request is embedded in the HTML form. This token is verified with every request.

### SameSite Cookie Attribute
Using the `SameSite` attribute in cookies can prevent CSRF attacks by ensuring that cookies are only sent in a first-party context.

### Checking the HTTP Referer Header
Validate that requests are coming from your website and not an external site.

### Using Custom Headers
Ajax requests can be protected by sending a custom header with the request.

## Conclusion
Understanding and preventing CSRF attacks is crucial for maintaining secure web applications. Developers should implement multiple layers of defense, including tokens, validation, and proper cookie management, to protect against CSRF vulnerabilities.
