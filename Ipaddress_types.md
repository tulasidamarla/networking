Computer networking and IP addresses
------------------------------------
Any computer(source host) process that interacts with another computer(desination host) process over internet needs reach the destination network, then destination host and the pid of the destination.

For ex, if the host computer wants to interact with www.google.com from browser, then it needs to get the ip(Internet protocol) from the DNS(Domain name service) server.

An IP address contains two parts named NID(network id) and HID(host id). Using NID request can reach destination network and using HID request can reach destination host. To interact with destination process, port number is required. By default, web servers run on 80. 

 DNS server translates domain names into IP addresses. Because it is easy to remember names than ipaddresses, we use names like google.com, yahoo.com etc. Every internet service provider has a DNS server, which will resolve domain to an ip address.
 
Everytime when a source wants to connect to a destination, it won't contact DNS, because of the overhead. The very first time, a host wants to resolve a new domain to an ipaddress, dns server will be contacted and the resulting ipaddress is cached.

In windows to see all the domains that are cached, execute the command ipconfig/displaydns.
In linux, it is available at /var/cache/nscd/hosts. To view the file "sudo strings /var/cache/nscd/hosts".

By default windows caches these dns entries for 86400 seconds. i.e. 1 day.

IP addresses are represented using 32 bit binary numbers also called dotted decimal representation. It contains 4 octets(8bits), each seperated with a dot(.). 

Out of 32 bits if 8 bits are used for NID and 24 bits are used for HID, then total no of networks we have is 2^8 . That means 256 and each network can have 2^24 (16 million) hosts. This is clearly not scalable. No one can purchase such a network because no enterperise contains 16m hosts.

To make the ipaddresses scalable for different needs, they were classified into different classes. 

Class A
-------
The total no of ipaddresses(2^32) are divided into two parts. The first part starts with 0 and second part starts with 1. The first part of ipaddresses fall under class A.

So, total no of ipaddresses we can have in Class A are 2^31.

In Class A 8 bits are used for NID and remaining 24 bits are for HID.

All Ip addresses that belongs to Class A fall into the range of 0 to 127. 0 and 127 are not used. So, no of available networks in Class A are 126. So, we can find out the Class of an ipaddress, by just looking at first octet in the ipaddress. For ex, If an ipaddress starts with 1,2,...126 it belongs to Class A network.

Note: Class A networks are generally purchased by very large enterprises like NASA, Pentagon etc.

In class A, we can have 2^7 or 128 (Because first bit 0 is fixed) networks and each network can have upto 2^24 (16 million) hosts.

Class B
-------
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

