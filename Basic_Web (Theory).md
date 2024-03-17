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

## Network Hardening
### Firewall
Filters Web Traffic based on based on predefined rules such as filtering ports or IPs.

### IDS (Intrusion Detection System)
Blocks Malicious Web Traffic
### IPS (Intrusion Prevention System)
Provided more Functionalities than IDS.

| Devices / Tools               | Advantages                                                  | Disadvantages                                                                            |
| ----------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Firewall**                  | - Allows or blocks traffic based on a set of rules.          | - Only able to filter packets based on information provided in the header of the packets. |
| **Intrusion Detection System (IDS)** | - Detects and alerts admins about possible intrusions, attacks, and other malicious traffic. | - Can only scan for known attacks or obvious anomalies; new and sophisticated attacks might not be caught. Doesn’t actually stop incoming traffic. |
| **Intrusion Prevention System (IPS)** | - Monitors system activity for intrusions and anomalies and takes action to stop them. | - An IPS is an inline appliance. If it fails, the connection between the private network and the internet breaks. Might detect false positives and block legitimate traffic. |
| **Security Information and Event Management (SIEM)** | - Collects and analyzes log data from multiple network machines. Aggregates security events for monitoring in a central dashboard. | - Only reports on possible security issues. Does not take any actions to stop or prevent suspicious events. |

