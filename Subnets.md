Subnets
--------
Dividing a network into smaller networks called subnets is needed for many practical purposes. For ex, having many departments in an organization etc.

Having subnets is useful interms of maintenance, and having different kinds of security to each subnet etc.

Having subnets changes the Network address, DBA. For ex, take a Class C ipaddress 
200.1.2.*. As we already know, In Class C we can have 2^8-2 hosts configured. If we divide this into two subnets, the first subnet address range from 200.1.2.0 to 200.1.2.127, the second subnet address range from 200.1.2.128 to 200.1.2.255.

For the first subnet, the network address is 200.1.2.0 and DBA is 200.1.2.127.<br>
For the second subnet, the network address is 200.1.2.128 and DBA is 200.1.2.255.

When a packet is sent to 200.1.2.255, does it broadcast to second subnet or the entire network?
It depends on where the packet is coming from. Generally, all subnets are connected to an Internal router. The Internal Router will identify, if a request is coming from with in the network or from outside the network. If a request comes from with in the netwokr, it broadcasts the packet to second subnet. If the request comes from outside, then it sends to all the subnets for broadcasting.

Everytime, when we create a subnet, two ipaddresses will be allocated, one for Network id and another for DBA. If we have to create 4 subnets, Then total no of ipaddresses available are 2^8 - 2*4 = 248.

Now an ip address contains a network id, Subnet id and Host id. For ex, consider the below id.
200.1.2.20 --> NID is 200.1.2.0 , Subnet ID is 00(First two digits octet) , host id is 010100(last six digits in the octet)

Subnet Mask
-----------
For ex, if we have 4 subnets in the network. Lets take the case of above example.
200.1.2.*. This ipaddress range is split into 4. i.e.
200.1.2.0 to 200.1.2.63<br>
200.1.2.64 to 200.1.2.127<br>
200.1.2.128 to 200.1.2.191<br>
200.1.2.192 to 200.1.2.255<br>

If a packet comes to say 200.1.2.20, how will the router identify which subnet to send the request?
The router uses subnet mask for this. Subnet mask will have all 1's in the network id part and subnet id part and all 0's in the host id part. For ex, In the above example
subnet mask is:

		11111111.11111111.11111111.11000000(255.255.255.192)

The subnet mask is used to identify the network. Let's see an example. Suppose we get a packet for 200.1.2.130. We need to do an AND operation of 200.1.2.130 with subnet mask to identify the network.

		11111111.11111111.11111111.11000000(255.255.255.192)
		11001000.00000001.00000010.10000010(200.1.2.130)
		-------------------------------------------------
		11001000.00000001.00000010.10000000(200.1.2.128)

The AND operation between the destination ip and subnet mask have given us the network id of the subnet which the destination ip belongs to. 

Routing
-------
Once the network id of a destination ip is found based on subnet mask, to route a specific subnet router uses routing table to forward the packet. For example, first subnet has network interface named a, second subnet has b, third subnet has c and fourth one is d. Then route table looks like this.

|Network ID	| Subnet mask   | Interface	|
|---------------|:--------:|:----------:|
|200.1.2.0 	 	|255.255.255.192|a    |
|200.1.2.64  	|255.255.255.192|b    |
|200.1.2.128 	|255.255.255.192|c    |
|200.1.2.192 	|255.255.255.192|d    |
|0.0.0.0 		|0.0.0.0		|e    |

If a request comes for ipaddress say, 200.1.2.90 router checks for the route table to identify the network it belongs. First, it checks for the first entry, if it doesn't match goes to the next entry and so on, until a match is found.

If no match is found, default entry is used. i.e. In the above example, the last entry represents default. All 0's represent any ip address.

Note:
There could be scenarios in which multiple networks can match a given ipaddress. In those scenarios, the netwokr with highest subnet mask is used. i.e. The subnet with more no of 1's.

Variable length subnet masking
------------------------------
In the above example, all subnets are of fixed length. i.e. each subnet contains same no of hosts. If we want to have 3 subnets say a,b,c with first one containing 128 nodes, second one contains 64 and third one also containing 64 nodes fixed length subnet masking won't help.

If the size of the subnets vary, then each subnet will get different length. This is called Variable length subnet masking(VLSM).

For the above requirement, we should choose something similary to IP address classes.
As we know, we can have 8 bits in the HID part for Class C, total no of hosts possible in this are 256. If we choose 1st bit for subnet mask identifier for first part, the remaining 7 bits can be used to configure hosts. In other words subnet a, contains subnet mask as 255.255.255.128(1 for the last octet's most significant bit).
Similary, for subnet b and c, Subnet mask would be 255.255.255.192(11 for the last octet's most significant bits).

It means, whenever subnet masks are different, the networks sizes are different.
Also, for a bigger network, subnet mask ipaddress will be smaller because it uses less no of bits to represent.

Routing table for this VLSM
----------------------------

|Network ID	| Subnet mask   | Interface	|
|---------------|:--------:|:----------:|
|200.1.2.0 	 	|255.255.255.128|a    |
|200.1.2.128  	|255.255.255.192|b    |
|200.1.2.192 	|255.255.255.192|c    |
|0.0.0.0 		|0.0.0.0		|d    |

Using subnet mask, we can identify how many ipaddresses are available in that subnet.
For ex, if 255.255.255.192 is the subnet mask, It means in the last octet we have binary number as 11000000. It indicates that remaining 6 digits are used to form the ipaddresses in the subnet. i.e. 2^6. We don't use first and last ipaddresses, so this subnet will have 62 ipaddresses.

Subnet mask problems
--------------------
No of hosts possible for a given subnet mask depends on no of ones present. For ex,
255.255.255.224 has total 27 1's. Remaining 5 bits are possible to configure hosts. So, total no of hosts are 2^5-2.

No of subnets possible depending on Class. For ex, Class A uses 8 bits for NID. Remaining bits are used for HID + SID. Consider the above example(255.255.255.224),<br> If Class A, then no of ones for SID is 19(27-8). It means for Class A, no of subnets possible are 2^19. <br>
For Class B, NID is 16 bits. So, no of ones in subnet are 11(27-16). Total no of subnets for Class B is 2^11.<br>
 For Class C, NID is 24 bits. So, no of ones in subnets are 3(27-24). Total no of subnets for Class C are 2^3.

Let's have a table to map binary to decimal numbers.

|Binary number	| Decimal   |
|---------------|:--------:|
|10000000 	 	|128		|
|11000000  		|192		|
|11100000  		|224		|
|11110000  		|240		|
|11111000  		|248		|
|11111100  		|252		|
|11111110  		|254		|


|Subnet Mask	| No of hosts   | Subnets(Class A)|Subnets(Class B)| Subnets(Class A)	|
|---------------|:-------------:|:---------------:|:--------------:|:------------------:|
|255.0.0.0 	 	|2^24-2    		|2^0   		      |N/A			    |N/A				|
|255.128.0.0  	|2^23-2    		|2^1	   		  |N/A			    |N/A				|
|255.192.0.0 	|2^22-2    		|2^2	   		  |N/A			    |N/A				|
|255.240.0.0	|2^20-2    		|2^4	   		  |N/A			    |N/A				|
|255.255.0.0	|2^16-2    		|2^8	   		  |2^0			    |N/A				|
|255.255.254.0	|2^9-2    		|2^15    		  |2^7			    |N/A				|
|255.255.255.0	|2^8-2    		|2^16   		  |2^8			    |2^0				|
|255.255.255.224|2^5-2    		|2^19   		  |2^11			    |2^3				|
|255.255.255.240|2^4-2    		|2^20   		  |2^12			    |2^4				|

Note: 255.0.0.0 is not a possible subnet mask for Class B and Class C. If it is Class B, it should have minimum 16 1's in the most significant bits. So, a Class B, subnet mask will start from 255.255.0.0. Similarly, for Class C subnet mask will start from 255.255.255.0.

Question
--------
Given the subnet mask 255.255.255.192 and ipaddress is 200.1.2.3, what is the size of the subnet and how many subnets are present?
Ans: No of 1's in subnet mask are 8+8+8+2 = 26. No of remaining bits are 32-26. So, size of the subnet is 2^6. Given Ip belongs to Class C. It means 24 bits for NID and 8 bits for SID+HID. SID bits 26-24. So, total no of subnets present are 4(2^2).























		
		
		
		





