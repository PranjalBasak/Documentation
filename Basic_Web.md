### Load Balancers

Load balancers act as middlemen, balancing web traffic among servers. They're also like doctors, checking the health of the servers to ensure smooth operations.

### CDN (Content Delivery Network)

CDNs function like clouds storing a server's static content, such as images and JS files, to reduce pressure on the local storage system.

### Databases

Databases serve as storage for various types of data, including user information, employee records, company details, and more.

### WAF (Web Application Firewall)

A WAF is akin to a security guard, preventing hacking attacks, including DDoS attacks, and ensuring the protection of servers.

### How Web Servers Work

#### What is a Web Server?

A web server is like a delivery guy for the internet. It listens for requests and uses the HTTP protocol to send web content to users. Common servers include Apache, Nginx, IIS, and NodeJS. They grab files from a set location on their hard drive, like /var/www/html for Nginx.

#### Virtual Hosts

Web servers host multiple sites using virtual hosts. They check the requested domain in HTTP headers, and if it matches a virtual host, the right site shows up. Each virtual host can point to a different folder on the hard drive, so one server can handle many websites.

#### Static Vs Dynamic Content

Static content never changes – think images, CSS, etc. They're served as-is. Dynamic content changes, like a blog homepage updating with new posts. Backend languages (PHP, Python, etc.) handle this dynamic stuff behind the scenes, making websites interactive.

#### Scripting and Backend Languages

Backend languages like PHP, Python, and NodeJS make sites interactive. They talk to databases, process user data, and more. For example, a basic PHP script can personalize a page based on your input without showing its code to you. But watch out – interactivity can bring security challenges! 🛡️
