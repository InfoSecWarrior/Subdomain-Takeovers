## Subdomain-takeovers

Subdomain takeover is a high-security vulnerability via which an attacker can control an expired management service from where the subdomain of the site was pointing

## What is that service?
It can be anything some of the vendors uses services like Shopify to build their shopping platform without changing their official subdomain you may have seen while shopping into some of the site something like powered by Shopify or something else this whole process of connecting one service to another is done by Cname.

## What is Cname and How it works -
Cname stands for the canonical name it is something that is related to hosting and domain connecting system so suppose you buy one domain from godaddy.com and hosting from hostinger.com for connecting this space we have things like nameserver did setup with nameserver and web services to get started this is the whole process apply on the name as well it is used to pointing one domain to another domain without getting the change with an actual subdomain.And if the name record expired then any malicious actor can perform a takeover
  ```                                                                                                                                                                                                                                           
$ subfinder -d Takeway.com > subdomain.txt
```

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

