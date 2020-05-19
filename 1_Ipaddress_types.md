# Computer networking and IP addresses

IP
-
- Any computer(source) process that interacts with another computer(desination) process over internet needs to reach the destination network, followed by destination computer, follwed by pid of the destination.
- If the source wants to interact with www.google.com from browser, it needs to fetch the ip(Internet protocol) from the DNS(Domain name service) server.
- An IP address contains two parts, NID(network id) and HID(host id). 
  -  NID is for reaching destination network 
  -  HID is for reaching destination host. 
- Port number is required for interacting with destination. web servers run on 80 by default. 

DNS
-
- DNS server translates domain names into IP addresses. 
- It is easier to remember names than ipaddresses. For ex, google.com, yahoo.com etc. 
- Every internet service provider has a DNS server, which will resolve domain to an ip address.
- When a source wants to connect to a destination, it won't contact DNS every time, because of the overhead. 
- If a host wants to resolve a new domain dns server will be contacted and the resulting ipaddress is cached.
- For windows to view all cached domains, execute the command from cmd prompt `ipconfig/displaydns`.
  - Expiry time for dns entries is 86400(1 day) by default.
- For linux, to view all cached domains, "sudo strings /var/cache/nscd/hosts".

IP address
-
- IP addresses are represented using 32 bit binary numbers, called dotted decimal representation. 
- An IP adress contains 4 octets(8bits), each seperated with a dot(.). 
- The first 8 bits are used for NID and 24 bits are used for HID.
  - Total no of networks possible are 256(2^8). 
  - Each network can have 16 million(2^24) hosts. 

IP address Classes
-
- The above network model is not scalable. No organization can purchase/maintain such a network with 16m hosts.
- To make IP addresses feasbible for different needs, they were classified into different classes. 

Class A
-
- Total no of IP addresses(2^32) are divided into two parts of 2^31 each.
- The first part that starts with 0 are class A IP addresses.
- Top most 8 bits are used for NID and remaining 24 bits are for HID.
- As the first bit is 0(for representing Class A), IP addresses have range of 0 to 127 is the first octet.
- Max no of networks in Class A are 126. 0 and 127 are not used.
- Max no of ip addresses in each network are 16 million(2^24).

Class B
-
- The second part of IP addresses that start with 1 are divided into two parts.
- The first part that starts with 10 are class B IP addresses.
- Most significant 16 bits are used for NID and the least significant 16 bits are for HID.


The remaining ipaddresses we have after class A are 2^31. These 2^31 ipaddresses are all have first bit 1. Now, these 31 bits are again divided into two parts. The first part starts with 0 and the second part starts with 1. So, Class B ip addresses fall under first part. That means all Class B ipaddresses start with 10.

No of ipaddresses in class B are 2^30. 

Class B ipaddresses use 16 bits for NID and 16 bits for HID. So, no of networks available are 2^14 or 16k. No of hosts in each network are 2^16-2 or 64000 because we don't use first and last ipaddresses.

As we know, Class B addresses start with 10, the first octet of class B addresses range from 10000000 to 11000000. That means Class B, ipaddresses range from 128 to 191.

Note: The total no of networks are 16k in Class B. But, we have ipaddress range from 128 to 191. It means, for each first octet there are 255 second octet values are available. That means In class B, 
128.0.*.* <br>
128.1.*.* <br>
...
128.255.*.*

Similarly, for ipaddresses that start with 129,130,..191 each will networks ranging from 0 to 255.

The practical users for these networks are like IRCTC, SBI etc.

Class C
-------
After Class A and Class B, the remaining ipaddresses are available are 2^30. These ipaddress start with 11. Now, the remaining 30 bits are again divided into two parts. The first part starts with 0 and second part starts with 1. Class C uses the first part. That means Class C ipaddresses start with 110.

No of ipaddresses in Class C are 2^29.

Class C ipaddresses use 24 bits for NID and 8 bits for HID. Because, the first 3(110) bits are fixed, with the remaining 21 bits, we can have upto 2 million networks in Class C. Each network can have 2^8-2 or 254 hosts because we don't use first and last ipaddresses.

As we know Class C starts with 110, ipaddresses range from 192 to 223.

The practical users of these networks are universities, small enterprises.

Class D
-------
After Class A,B and C, the remaining bits are 29. Again these are divided into two parts. The first part start with 0. These fall under Class D. so, all ipaddresses of Class D start with 1110.

No of ipaddresses in Class D are 2^28.

Class D ipaddress range from 224 to 239. These are not divided into NID and HID. These are not used for normal purposes. Class D addresses are used for multicasting or broadcasting.

Class E
-------
After Class A,B,C and D, the remaining ipaddresses(2^28) available fall under Class E.
So, all ip addresses of Class E start with 11110.

No of ipaddresses in Class E are also 2^28, because they were not divivded further.

Class E ipaddress range from 240 to 255. These are not divided into NID and HID. These are not used for any practical purposes.

Note: Class D is a disadvantage because there 256 millions available, even today we have less than 1000 groups who does this.

