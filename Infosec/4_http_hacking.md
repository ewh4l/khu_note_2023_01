- web application << web site
	- "web site running web-application"

- The big picture (pg.3)

- apache, nginx -> repsond for static info requests(html, css ..)


### Directory listing
- Was a functionality
- Accessing un-authorized dirs.

### Local File Inclusion
- Adding `?page=../../../../../WINDOWS/system32/drivers` behind url
	- GET request param

### .htaccess
- quite old vuln

### Upload vulnerability
- Upload 
	- e.g. adding file to an email
- Hiding real extension
	- e.g. `backdoor.php.png`
- Getting the "web-shell"

### **Web-shell**
- A Program injected by attacker after penetration succeeds. 
- Permanent backdoor
- Often built using PHP.

### SQL injection

### XSS
- Circumvent SOP(Same-Origin-Policy)
- Insert malicious JS to be executed from users.

### CSRF

### http & https
- https = http + SSL/TLS
- new : `ftp://blabla`