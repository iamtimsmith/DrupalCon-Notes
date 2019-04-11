# Cracking Drupal

> ## Peter Wolanin & Michael Hess
>
> - Drupal security team members since 2008/2011
> - Core contriubutors for 5, 6, 7, 8

## Agenda

- Review top 10 types of vulnerabilities
- Learn best practices
- Answer Questions
- Have fun

## CIA Triad

- Confidentiality, integrity, availability (CIA)
- Model designed to guide policies for information security within an organization
- Model is also referred to as AIC triad (availability, integrity, and confidentiality) to avoid confusion with Central Intelligence Agency

## OWASP Top 10

- Open Web Application Security Project
- List of most critical security risks
- Assessment of attack vector, weakness
- Updated every few years, 2017 is the latest
- [owasp.org](https://wwww.owasp.org)

## What types of Vulnerabilities

1. Injection
1. Broken Auth
1. Sensitive data exposure
1. xml eternal entities (XXE)
1. Broken access control
1. Security

## 1. Injection

- Attacker's input is directly interpreted as code
- Most severe kind of attack
- Allows hacker to compromise site, server, or other apps on same server
- Could be used to insert new data, new role, modify content, or do whatever they want with db
- Examples
  - SQL Injection
  - via Form API
  - phar file execution
  - unserialization
- Users could:
  - Pull email addresses from db
  - All content (even unpublished) is available
  - Potentially add js to capture passwords
  - Gain root access on the server

## 2. Broken Authentication

- Choose good passwords, use TFA for admins (preferably all users)
  - drupal.org/project/password_policy
  - drupal.org/project/tfa
- Hash passwords (Drupal core covers this)
- Protect session IDs
  - Set up HTTPS. Don't send unencrypted session IDs
  - All HTTPS should be used for sites now

## 3. Sensitive Data Exposure

- **Encrypt sensitive data** such as credit cards in db. Don't store if you don't have to (PCI, HIPPA, etc)
- Know your risk level
- Weak keys or poor key management can still expose
- Use **HTTPS** for all traffic
- User **passwords** are properly hash-salted by Drupal 7.x+ core, but weak passwords can still be cracked

## 4. XML External Entities (XXE)

- May be used to expose private or system file content, conduct a DoS attack, scan local networks, etc.
- Affects SOAP, SAML, OPML feeds or anywhere else where XML is parsed.
- XML parsers may allow external entities by default, but beware of vendor libraries. Consider source of XML being parsed.

## 5. Broken Access Control

- Category: Access bypass vulnerabilies.
  - Anonymous user can see stuff they shouldn't be able to.
- Happens rarely for Drupal core, just use the user permissiona nd access APIs.
- Example: A custom page cb that displays a node without checking node access.
- Easy to fix, usually a setting in a hook which either needs to be set to permission level or set to `true/false`

## 6. Security Misconfiguration

- Display of PHP error reporting
  - Disable at `/admin/config/development/logging`
- PHP filter module, disbale at `/admin/modules`
- PHP files writeable by the web server
- Write permissions for `www-data` pose a risk
- Permissions
  - Be careful with restricted, site-owning permissions (which roles do you trust?)
  - Same for text formats (full HTML == XSS)
  - Do not use the user 1 account in daily work, it has all permissions. Best practice to block account
  - User 1 name should not be `admin` or any other easily guessable name
- Private files configuration
  - Move the private files directory outside of the docroot to avoid direct downloads
- PHP file execution
  - Drupal uses the front controller pattern: almost everything goes through `index.php`
  - Disallow execution of PHP files in subfolders
  - Prevents PHP execution in files directory
  - Apache Example: `RewriteRule "^.+/.*\.php$" - [F]`
  - Nginx exmaple: `location ~* ^.+/.*\.php$ { deny: all }`

## 7. Cross-Site scripting (XSS)

- Attackers can inject JS tags
- All user input must be sanitized before printing HTML
- (admin) user interaction is required - beware redirects
- Persistent XSS
  - Attackers JS is stored in the DB.
  - Vulnerable code, because of the node title
- XSS is _REALLY_ Dangerous
  - Some people assume that the common test for XSS, an alert is the actual attack (this is wrong)
  - Anything that you as admin can do, XSS can do also - change settings, passwords, user roles, etc.
- Filtering on output
  - When handling data, the golden rule is to store **exactly** what the user typed.
  - When user edits post, form should contain all the same stuff as when they first submitted it.
  -
- Mitigating XSS
  - What Drupal core does for us:
    - Sets HTTPOnly flag on session cookies to prevent JS
    - Password change requires current password
    - Text formats for different user roles
    - Autoescape in D8
  - Content Security Policy: W3C standard, no inline js execution & JS domain whitelist
  - We still need to rigorously escape user input

## 8. Insecure Deserialization

- Unserialization can be exploited in PHP via magic methods like `__destruct()` to delete files or even execute code.
- SA-CORE-2019-003 was a result of serialized strings being parsed for some fields as part of API calls.
- Never use PHP serialize format for cookies, form data, etc. - use a safe format like JSON.

## 9. Using Components with Known Vulnerabilities

- Widespread attack vectors, often automated
  - Update all server software regularly
  - Monitor security mailing lists, RSS feeds, etc.
  - Enable Drupal's update status notifications and emails
  - Security advisories at https://drupal.org/security
  - Disable software components (like modules) that are not used
- Current Versions:
  - Drupal 7 EOL in 11/2021
  - Drupal 8 EOL is 11/2021 but will be easier to upgrade
  - Both of these will be considered outdated components and could see some vulnerabilities after third parties take over.

## 10. Insufficient Logging & Monitoring

- **What is happening to your durpal sites right now?** If you were experiencing unusual requests or logins, would you know, or be able to find out later?
- If the Druapl or system logs were deleted, do you have a central copy?
- Recent high-profile hacks were potentially going on for months before being detected
- Read your logs!
  - Use services that help with finding abnormalities
  - Have central logging

## Not Top 10

- Cross-Site request Forgery (CSRF)
  - Attacker posts comment
  - Chain of attack
    - Logged in dmin visits content page
    - Browser fetches image src and sends cookies
    - Req
  - Protecting agaainst CSRF
    - Write operation need to be protected. Use wither:
      - Confirmation forms
      - Security tokens in URL
    - POST request: alwasy use Form API! JS can execute CSRF POST attacks or you might submit a form on a malicious website.
    - Docs: drupal.org/node/178896

## Do you see the pattern?

- Dont trust user provided data in URL, request, or content in DB
- Attackers use browser features to perform actions behind user's back (XSS, CSRF, open redirects).
- Attackers use known vulnerabilities and automated tools to mass-hijack sites.

## Be Prepared for an attack

- Is your code in version control (git, svn, etc)
- How often do you make full **backups**?
- Do you have separate login for each admin?
- If you are responsible for server (or VPS / VM) software do you keep it up to date?
- Do you have an out-of-band access method (e.g. ssh + drush vs web login)?
- Do you know where to find the Drupal watchdog log, web server log, syslog, etc?

## How to recover from an attack

- Best thing you can do is rebuild your site
- Determine what was compromised and when - after making a copy fo the site
- Restore from backup
- Update code (and server software)
- Change all passwords and keys
- Audit your code (custom modules first!)
- Save and then scan logs for traces of the attacker (Drupal watchdog log, web server log, syslog, etc)

## Useful Security Modules

- Security Review
- Paranoia
- Seckit

## Security improvements in D8

- Twig auto-escap in templates
- Forbid PHP file executions
- PHP module was removed from core

## Your hosting matters

- Is your primary business hosting? If not pay someone to do it. It's not secure.
- Shared hosting gives access via cPanel
- Unless you understand multisite really well, don't use it.
