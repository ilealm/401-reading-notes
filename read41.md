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

# Source
[Source - Wikipedia](https://en.wikipedia.org/wiki/Web_application_security)