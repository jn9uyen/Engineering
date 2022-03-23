# Internet / Web Server Notes

## [What is the difference between port 80 and 8080?](https://askinglot.com/what-is-the-difference-between-port-80-and-8080)

Port 80 is the default port. It's what gets used when no port is specified. 8080 is Tomcat's default port so as not to interfere with any other web server that may be running. If you are going to run Tomcat as your web server, the port can be changed to 80 so that visitors do not need to specify it.

### In this manner, what is the port 8080?

Port 8080 is commonly used as proxy and caching port. It is also above the service port range. Port 8080 also can run a Web server as a nonroot user. Other assignments for port 8080 include Apache Tomcat, an M2MLogger and a Web GUI.

### What port can I use instead of 80?

Since port 80 is not an option, you need to find an alternative port. There is no official HTTP alternative port. When port 80 is used for one address/webserver, it's fairly common to use port 8080 or 8000 for another site on the same address/webserver.

### In this manner, should I use port 80?

You could theoretically use any ports that are not already in use or blocked by a firewall (higher port 1024 is usually pretty safe; higher than port 10000 is almost certainly safe).

- **Port 80** is the default for unencrypted HTTP traffic
- **Port 443** is the default for encrypted HTTPS traffic.

### Is it safe to open port 8080?

8080 is not secure. In TCP/IP security is a layer that has to be added. In simple terms you have to enable SSL to make 8080 secure. Once you add SSL then all ports become secure i.e. even ftp, smtp, http, etc.

### [Should I run my small website in port 80, 8080, or 81?](https://superuser.com/questions/720641/should-i-run-my-small-website-in-port-80-8080-or-81)

There are two things to consider here:

1. Will your users remember to use a non-standard port in the name? By default, port 80 is the standard and therefore you do not have to type it into the URL. For example, http://superuser.com runs on port 80 and your browser assumes 80 is the port you mean when typing it in. It is no different than typing http://superuser.com:80. If you run your websever on port 8080, then the user has to type http://superuser.com:8080. The average user will not likely remember that.
2. Does running a webserver on a non-standard port protect you from DoS attacks? Not really. If someone really wanted to bring your site down, running on a non standard port will not stop them. Attackers will scan all the ports on your IP and quickly find that 8080 (or whatever you choose) is open and responding to HTTP requests.
Methods like changing ports is called "Security through obscurity" and it is highly questionable that the extra work and inconvenience provides any valuable security.

## [Localhost](https://sitebulb.com/hints/links/has-link-with-a-url-referencing-localhost-or-127001/#:~:text=LocalHost%20is%20the%20standard%20host,0.1.)

LocalHost is the standard host name given to the address of the local computer, and the IP address for your localhost is **127.0.0.1**. The local server isn't connected to the internet, but makes it possible to see your site in the browser as if you're viewing it online - so LocalHost addresses may be used during development of a website.

## [Localhost Definition 2](https://whatismyipaddress.com/localhost)

- The localhost is the default name describing the local computer address also known as the loopback address. For example, typing: `ping localhost` would ping the **local IP address of 127.0.0.1** (the loopback address). When setting up a web server or software on a web server, `127.0.0.1` is used to point the software to the local machine.
- In computer networking talk, localhost refers to “this computer” or even more accurately “the computer I’m working on.” IT types, network administrators and programmers, will even use the term “home” (home computer). A key word in this definition is “network,” because the term localhost comes into play only when someone (such as a programmer) is at their computer, connected to a network and using it to test programs or to test the virtual connection between two computers.

Not just a name, but a number too. Don’t let that confuse you. It’s not much different from you typing in Disney.com or Amazon.com in your browser’s address bar. Every website has its own IP address, but you substitute a “domain name” instead. So, when an IT person is running tests and he’s “telling” an application to connect to the Internet, he’ll type in the destination “localhost.” In other words, he can pretend to be connecting to a Web server or another host computer, but he’s keeping it in-house and close to home by using localhost.

On almost all networking systems, localhost uses the IP address 127.0.0.1. That is the most commonly used IPv4 “loopback address” and it is reserved for that purpose. The IPv6 loopback address is ::1.
