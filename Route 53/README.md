##### DNS
+ Domain Name System which translates the human friendly hostnames 
into the machine IP addresses
+ www.abc.com => 172.1.2.3
+ DNS is the backbone of the Internet
+ DNS uses hierarchical naming structure
+ eg: api.example.com

##### DNS Terminology

+ Domain Registrar: Amazon Route 53, GoDaddy, …
+ DNS Records: A, AAAA, CNAME, NS, …
+ Zone File: contains DNS records
+ Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
+ Top Level Domain (TLD): .com, .us, .in, .gov, .org, …
+ Second Level Domain (SLD): amazon.com, google.com,
+ Zone file: Contains DNS records
+ Name Server: A server responsible for resolving DNS queries by translating domain names into IP addresses. They can be authoritative (containing the original zone file) or non-authoritative (caching DNS records from other name servers).
+ Top-Level Domain (TLD): These are the highest levels of the domain name hierarchy, e.g., .com, .org, .net, .edu, .gov, .uk, .in, etc. They are managed by various organizations and registrars.
+ Second-Level Domain (SLD): These are the domains directly before the TLD, such as "example" in example.com or "amazon" in amazon.com. They are unique and registered by organizations or individuals.

<img src="images/DNS terminology.png" height='100%' width='100%'>

<img src="images/DNS work.png" height='100%' width='100%'>

##### Amazon Route 53
+ A highly available, scalable, fully
managed and Authoritative DNS
+ Authoritative = the customer (you)
can update the DNS records
+ Route 53 is also a Domain Registrar
+ Ability to check the health of your
resources
+ The only AWS service which
provides 100% availability SLA
+ Why Route 53? 53 is a reference to
the traditional DNS port