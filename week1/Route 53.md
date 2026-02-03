![WhatsApp Image 2026-01-25 at 8 50 08 PM](https://github.com/user-attachments/assets/37e72461-1527-4edb-b1cb-466bc20012df)
[Route53_Notes.txt](https://github.com/user-attachments/files/25044980/Route53_Notes.txt)

1. What is DNS?
DNS - Domain Name System, translates human readable domain names(for eg. wwww.amazon.com) to machine readable ip addresses (for eg. 192.0.2.44). When you open a web browser and go to a website, you don't have to remember and enter long number.

DNS default port number 53. Hence we calling this service as Route53.

We can either purchase Domain from AWS/3rd party provider.

DNS should be globally unique one

2. Show the paint and explain 
3. Created hosted zone -->type domain name --> choose public hosted zone --> once you created hosted zone --> will see the four name servers--> go and paste the four name servers in go daddy.

Go daddy --> Provide Domain name
Route 53 --> Provide four name servers

4. It is global service.
5. Create 3 ec2 instance

#! /bin/bash
yum install httpd -y
service httpd start
echo "This is my Route53 Application" > /var/www/html/index.html

6. Copy the ip address and hit in the browser

NOTE:
now as per the paint elb DNS configuration
if you want to enable elb-->go to records --> enable alias name --> choose route traffic to(Alias to application and classic load balancer) --> choose region -->select load balancer
7. Go to Hosted zone --> create records -->change the Alias icon -->choose route traffic to Alias to Application and Classic Load balancer --> Choose region -->Okay

8. TTL --> Time to leave -->60 sec they need to give response
DNS Propagation time --> 72 hrs
9. Instead of hit the ip address u just enter domain name you can see the output.
10. Types of Routing policy:
1. Simple Routing policy
2. Weighted Routing policy
3. Geolocation routing policy
4. Latency routing policy
5. Failover routing policy
6. Multivalue routing policy

1. Simple routing policy:

When there is only one web server we will use this policy.
1. Create instance with sample application into user data

#! /bin/bash
yum install httpd -y
service httpd start
echo "This is my Route53 Application" > /var/www/html/index.html

2. Purchase a domain from Route 53 on from 3rd part provider.
3. Create Hosted zone --> Provide domain name --> Public hosted zone
4. Get the name servers --> change it inside GoDaddy nameservers.
5. Now try the domain name in browser and confirm the output of application.
(Atlast delete the record set of simple routing policy)

2. Weighted Routing policy:

 This policy used according to the weightage of the server. We have two instance 1). Primary server 2) Secondary server
1. Rename the instance to show the difference
2. Create Record --> Provide ip address(1st machine) --> change the TTL to 1min (for Quickoutput) --> change the routing policy to weighted --> set the weight(0 to 255) --> Give the name for Record ID(this should represent the configuration of the machine)
3. Create another record --> Provide 2nd machine IP addresses--> Complete the step
4. Try giving command in command prompt(nslookup [domainname]), so that it will show the IP address of the machine accordingly.
(Atlast delete the record set of weighted routing policy)

3. Geolocation Routing policy:
The server can be routed according to the location, and denial of certain website can be configured by restricting the location.
1. Rename the instance to show the difference
2. Create Record --> provide IP address(India machine) to change the TTL to 1 min(for quicker output) --> change the routing policy to geolocation--> select the regions as India --> Give name for RecordID(this should represent the region of the machine)
3. Create another record --> provide 2nd location -->IP Address --> Complete the steps
4. Try giving command in command prompt(nslookup [domainname]), so that it will show the IP address of the machine according to region.
(Atlast delete the record set of Geolocation routing policy)

4. Latency Routing policy:
This will reach the nearby server and give me the output.
1. Rename the instance to show the difference
2. Create record --> provide ip address(Mumbai machine) --> Change the TTL to 1min (for Quicker output) --> change the routing policy to latency --> select the region as Mumbai --> Give name for RecordID(this should be related to the content of the machine)
3. Create another record --> provide 2nd location(singapore) IP address --> complete the steps
4. Try giving command in command prompt(nslookup [domainname]) so that it will show the ip address of the machine according to the latency.
(Atlast delete the record set of Latency routing policy)

5. Failover Routing policy:

If any primary server got failed it will automatically pickup the secondary server we need to maintain 2 different server under 2 different location.

1. Rename the instance to show the difference
2. Create Health check name it --> provide the primary machine ip --> give host name(www.example.com) --> path(index.html) --> set notification if needed
3. Create record --> provide ip address(primary machine) --> change the TTL to 1 min(for Quicker output) --> change the routing policy to failover  --> set the failover type as primary --> Enable health check as primary --> Give name for recordID(this should related to the content of the machine)
4. Create another record --> provide secondary IP address --> set the failover type as secondary --> (Don't enable health check for secondary machine) --> complete the steps
5. Now manually terminate the primary instance so that it should be re-route to the secondary server.
6. Try giving command in command prompt(nslookup [domainname]) so that it will show the secondary ip address of the machine.
7. Delete the record set of failover routing as well as Health check.
8. (Atlast delete the record set of Failover routing policy)
(Delete the Hosted zone for avoiding the charges)

Example:
SRP --> It is used only for testing purposes
WRP --> Ansibe tool master slave concept
GRP --> If you want to block the application in other country so we can go with policy.
LRP --> To get the immediate output bu using nearby server
FRP --> We used this policy in realtime application mostly 


