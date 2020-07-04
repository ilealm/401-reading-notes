[ HOME ](README.md)
# Read - Web Application Security

> Web application security is a branch of information security that deals specifically with security of websites, web applications and web services. 


- The majority of web application attacks occur through cross-site scripting (XSS) and SQL injection attacks.


### Top Vulnerabilites


- 37%	Cross-site scripting (XSS)
- 16%	SQL injection
- 5%	Path disclosure
- 5%	Denial-of-service attack
- 4%	Arbitrary code execution
- 4%	Memory corruption
- 4%	Cross-site request forgery
- 3%	Data breach (information disclosure)
- 3%	Arbitrary file inclusion
- 2%	Local file inclusion
- 1%	Remote file inclusion
- 1%	Buffer overflow
- 15%	Other, including code injection (PHP/JavaScript), etc

#### Cross-site scripting (XSS)

> "XSS" redirects here. For other uses, see XSS (disambiguation).

Cross-site scripting (XSS) is a type of web application security vulnerability typically found in web applications. XSS attacks enable attackers to inject client-side scripts into web pages viewed by other users. A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same-origin policy. Cross-site scripting carried out on websites accounted for roughly 84% of all security vulnerabilities documented by Symantec up until 2007.[1] In 2017, XSS attacks were still considered a major threat vector.[2] XSS effects vary in range from petty nuisance to significant security risk, depending on the sensitivity of the data handled by the vulnerable site and the nature of any security mitigation implemented by the site's owner network.


#### SQL injection 
SQL injection is a code injection technique, used to attack data-driven applications, in which malicious SQL statements are inserted into an entry field for execution (e.g. to dump the database contents to the attacker).[1] SQL injection must exploit a security vulnerability in an application's software, for example, when user input is either incorrectly filtered for string literal escape characters embedded in SQL statements or user input is not strongly typed and unexpectedly executed. SQL injection is mostly known as an attack vector for websites but can be used to attack any type of SQL database.



## Best practices recommendation

Secure web application development should be enhanced by applying security checkpoints and techniques at early stages of development as well as throughout the software development lifecycle. Special emphasis should be applied to the coding phase of development. Security mechanisms that should be used include, threat modeling, risk analysis, static analysis, digital signature, among others.




## Security technology

0There are a number of technical solutions to consider when designing, building and testing secure web applications. At a high level, these solutions include:

- Black box testing tools such as Web application security scanners,vulnerability scanners and penetration testing software.
- White box testing tools such as static source code analyzers.
- Fuzzing, tools used for input testing.
- Web application security scanner (vulnerability scanner).
- Web application firewalls (WAF), used to provide firewall-type protection at the - web application layer.
- Password cracking tools for testing password strength and implementation.


# Security in Django


### Cross site scripting (XSS) protection
XSS attacks can originate from any untrusted source of data, such as cookies or Web services, whenever the data is not sufficiently sanitized before including in a page.

Using Django templates protects you against the majority of XSS attacks. Django templates escape specific characters which are particularly dangerous to HTML. While this protects users from most malicious input, it is not entirely foolproof. For example, it will not protect the following:

`<style class={{ var }}>...</style>`

If var is set to `'class1 onmouseover=javascript:func()'`, this can result in unauthorized JavaScript execution, depending on how the browser renders imperfect HTML. 


It is also important to be particularly careful when using is_safe with custom template tags, the safe template tag, mark_safe, and when autoescape is turned off.

In addition, if you are using the template system to output something other than HTML, there may be entirely separate characters and words which require escaping.

You should also be very careful when storing HTML in the database, especially when that HTML is retrieved and displayed.

###  Cross site request forgery (CSRF) protection

CSRF attacks allow a malicious user to execute actions using the credentials of another user without that user’s knowledge or consent.

Django has built-in protection against most types of CSRF attacks, providing you have enabled and used it where appropriate. However, as with any mitigation technique, there are limitations. 

CSRF protection works by checking for a secret in each POST request. This ensures that a malicious user cannot “replay” a form POST to your website and have another logged in user unwittingly submit that form. The malicious user would have to know the secret, which is user specific (using a cookie).

When deployed with HTTPS, CsrfViewMiddleware will check that the HTTP referer header is set to a URL on the same origin (including subdomain and port). Because HTTPS provides additional security, it is imperative to ensure connections use HTTPS where it is available by forwarding insecure connection requests and using HSTS for supported browsers.

Be very careful with marking views with the csrf_exempt decorator unless it is absolutely necessary.

### SQL injection protection


Django’s querysets are protected from SQL injection since their queries are constructed using query parameterization. A query’s SQL code is defined separately from the query’s parameters. Since parameters may be user-provided and therefore unsafe, they are escaped by the underlying database driver.

Django also gives developers power to write raw queries or execute custom sql. These capabilities should be used sparingly and you should always be careful to properly escape any parameters that the user can control. In addition, you should exercise caution when using extra() and RawSQL.

### Clickjacking protection

Clickjacking is a type of attack where a malicious site wraps another site in a frame. This attack can result in an unsuspecting user being tricked into performing unintended actions on the target site.

Django contains clickjacking protection in the form of the X-Frame-Options middleware which in a supporting browser can prevent a site from being rendered inside a frame. It is possible to disable the protection on a per view basis or to configure the exact header value sent.

The middleware is strongly recommended for any site that does not need to have its pages wrapped in a frame by third party sites, or only needs to allow that for a small section of the site.

### SSL/HTTPS

It is always better for security to deploy your site behind HTTPS. Without this, it is possible for malicious network users to sniff authentication credentials or any other information transferred between client and server, and in some cases – active network attackers – to alter data that is sent in either direction.

If you want the protection that HTTPS provides, and have enabled it on your server, there are some additional steps you may need:

If necessary, set SECURE_PROXY_SSL_HEADER, ensuring that you have understood the warnings there thoroughly. Failure to do this can result in CSRF vulnerabilities, and failure to do it correctly can also be dangerous!

Set SECURE_SSL_REDIRECT to True, so that requests over HTTP are redirected to HTTPS.

Use `‘secure’` cookies.

## Host header validation

Django uses the Host header provided by the client to construct URLs in certain cases. While these values are sanitized to prevent Cross Site Scripting attacks, a fake Host value can be used for Cross-Site Request Forgery, cache poisoning attacks, and poisoning links in emails.

Because even seemingly-secure web server configurations are susceptible to fake Host headers, Django validates Host headers against the ALLOWED_HOSTS setting in the django.http.HttpRequest.get_host() method.

This validation only applies via get_host(); if your code accesses the Host header directly from request.META you are bypassing this security protection.

# Sources
[Source - Wikipedia](https://en.wikipedia.org/wiki/Web_application_security)
[Security in Django](https://docs.djangoproject.com/en/3.0/topics/security/#security-in-django)