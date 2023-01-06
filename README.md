## Subdomain Takeover

Subdomain takeover is a type of attack that allows an attacker to control a subdomain that is not properly configured. This can happen if a subdomain is pointed to a service (e.g., GitHub pages, Heroku, etc.) that has been deleted or no longer belongs to the organization.

An attacker can then set up a page on the service that was previously being used by the subdomain, and use it to serve malicious content or conduct phishing attacks. Subdomain takeover can be difficult to detect and can have serious security implications for an organization. It is important to regularly check for and properly configure subdomains to prevent this type of attack.

## What is vulnerbility due to which subdomain takeover occurs

A subdomain takeover vulnerability occurs when a subdomain (e.g., "test.example.com") is pointed to a service (e.g., GitHub pages, Heroku, etc.) that has been deleted or is no longer associated with the organization. This can happen if the organization was previously using a third-party service to host content for the subdomain, but the service was later decommissioned or the account was deleted. If the DNS record for the subdomain is not properly updated to point to a new location, an attacker may be able to register an account with the same name on the service and set up a page that is served from the subdomain.
To prevent subdomain takeover vulnerabilities, it is important to regularly check for and properly configure subdomains, and to ensure that DNS records are updated when a service is no longer in use. It is also a good idea to monitor for any unexpected changes to subdomains, as this may be a sign of an attempted takeover.

## What is Cname and 

CNAME (Canonical Name) is a type of DNS record that is used to alias one domain name to another. It is often used to redirect traffic from one subdomain (e.g., "www.example.com") to another subdomain (e.g., "app.example.com"), or to point a subdomain to a third-party service (e.g., GitHub pages).

## Here's how CNAME works:

A user enters a domain name into their web browser (e.g., "www.example.com").
The browser sends a request to the DNS server to look up the IP address for the domain.
The DNS server responds with the IP address for the domain, or with a CNAME record that points to another domain.
If the DNS server returns a CNAME record, the browser sends a new request to the DNS server to look up the IP address for the domain specified in the CNAME record.
The DNS server responds with the IP address for the second domain, and the browser connects to the server at that IP address.
                                                                                                                                                          
  ## step 1
     ## Subfinder for finding subdomain
  
$ subfinder -d Takeway.com > subdomain.txt
## Step 2
## MassDns to find Subdomain Cname

```
$ massdns -r resolvers.txt -t CNAME  -o S  -w scope-CNAME.txt subdomain.txt
```

## Step 3
## Grep 3rd party services 

![image](https://user-images.githubusercontent.com/94091556/210230175-e4572147-f579-4c31-bd7b-c34f1172d4dd.png)

   ```                                                                                                                                                                                                                                           
$ cat scope-CNAME.txt | grep -v -e"takeaway\.com\.$" | cut -f 3 -d" " | sed 's/.$//g' 

thuisbezorgdbeta.hypernode.io
geomaps.takeaway.com.s3.amazonaws.com
```

## Use nuclei for detect vulnerability


![image](https://user-images.githubusercontent.com/94091556/210229808-80e28302-8248-4598-b6d5-d08e220e580c.png)

   ```                                                                                                                                                                                                                                           
$ nuclei -l Cname.txt -t /home/rooter/Desktop/nuclei-templates/takeovers
```
## Cross check venerable Domain CNAME

![image](https://user-images.githubusercontent.com/94091556/210229908-7f4a8cad-752a-45ff-9f5a-bebeeec0fc14.png)

                                                                                
```
$ dig images.takeaway.com
```
## check Cname webserver search
![image](https://user-images.githubusercontent.com/94091556/210230072-ef4020a6-4813-4d21-a019-37d7f81be902.png)

