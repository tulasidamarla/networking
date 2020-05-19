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
- The range that starts with 0 are class A IP addresses.
- Most significant 8 bits are used for NID and the least significant 24 bits are for HID.
- Any IP address in the range of 0 to 127 in the first octet belongs to Class A.
- Max no of networks in Class A are 126. 0 and 127 are not used.
- Max no of ip addresses in each network are 16 million(2^24).

Class B
-
- The second part of IP addresses that are remaining after Class A are divided into two parts.
- The first part that starts with 10 are class B IP addresses.
- Total no of Ip addresses in Class B are 2^30.
- Most significant 16 bits are used for NID and the least significant 16 bits are for HID.
- Any IP address in the range of 128 to 191 in the first octet belongs to Class B.
- Max no of networks in Class B are 2^14(16k).
- Max no of hosts in a Class B network are 2^16-2(64k appx).
- The ip address range for Class B are 

      128.0.*.* <br>
      128.1.*.* <br>
      ...
      128.255.*.*
      129.0.*.* <br>
      129.1.*.* <br>
      ...
      129.255.*.*
      ...
      ...
      191.0.*.* <br>
      191.1.*.* <br>
      ...
      191.255.*.*

Class C
-
- The ipaddress remained after Class A and Class B are 2^30. These bits are again divided into two ranges.
- The ip address range that start with 110 are Class C.
- Most significant 24 bits are for NID and the lease significant 8 bits are for HID.
- Total no of ip addresses in Class are 2^29.
- Total no of networks are 2^21(2 million) becuase the first 3 bits 110 are fixed.
- Total no of hosts are 2^8-2(254)
- Any IP address in the range of 192 to 223 in the first octet belongs to Class C. 

Class D
-
- After Class A, B and C the remaining bits are 29. These ip addresses are divided into two ranges. 
- The ip address range start with 1110 are Class D.
- Total no of ipaddresses in Class D are 2^28.
- Any IP address in the range of 224 to 239 in the first octet belongs to Class D. 
- These are not divided into NID and HID.
- These are used for multicasting and broadcasting.


Class E
-------
- After Class A, B, C and D,  the remaining bits are 28.
- The ip address range start with 1111 are Class E.
- Total no of ipaddresses in Class D are 2^28.
- Any IP address in the range of 240 to 255 in the first octet belongs to Class E. 
- These are not divided into NID and HID.
- These are used for multicasting and broadcasting.
- These ip addresses are not used for any practical purposes.


