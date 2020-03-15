All Ip addresses are assigned by IANA(Internet Assigned Number Authority).

Problems With Classful IP addresses
-----------------------------------
If an enterprise want to have some 100 public ip addresses, there is no way other than purchasing Class C network, which will give 256 ipaddresses.

Classless IP addresses are for rescue. If we want to purchase 100 ipaddresses, it is possible with Classless. In Classless, we call these ipaddress ranges as blocks instead of networks. So, a classless ipaddress contains BID(blockid) and HID. 

Based on ipaddress, we can't figure out howmany bits are used BID. To solve this problem, CIDR notation is a little different from standard ipaddress notation.

CIDR notation is a.b.c.d/n -> where n represents no of bits in BID.For ex,if 20.10.1.2/20, is the CIDR, then it represents 20 bits are used for BID. So, no of bits in the block are 32-20=12. No of hosts in the block are 2^12.

Rules for forming CIDR blocks
-----------------------------
1)All the ipaddresses are contiguous.
2)Block should be alwasy 2 power n. You can ask for 128 ipaddresses, you cannot ask for 100.
3)First ip address in the block should be evenly divisible by block size.

The Reason for choosing 2 power n.
----------------------------------
Let's take an example of 1011(Decimal 11) dividing by 2.


|Binary number	| Divider	    | Remainder		  |Quotient		   |
|---------------|:-------------:|:---------------:|:--------------:|
|1011	 	 	|2^1    		|1   		      |5(101)		   |
|1011  			|2^2    		|3(11)	   		  |2(10)		   |
|1011  			|2^3    		|3(101)	   		  |1(1)			   |
|1011  			|2^2    		|4(1011)   		  |0			   |

From the above example, it is clear that if you divide a number by 2 power n, The most significant least significant n bits of the binary number are remainder, remaining are quotient. So, If you have m bit binary number, and you divide that number with 2 power k, the least significant k bits represent represent remainder, remaining numbers represent quotient.

So, it is easy to choose BID and HID part of the ipaddress, if we choose block size as 2 power of n, then we can completely utilize the HID part for allocating contiguous addresses.

The Reason for choosing evenly divisible by block size.
-------------------------------------------------------
For ex, if the block size(or HID) is 2^5, then the first ip address in the block if you divide by 32(2^5), the remainder will be 0 because we know remainder is the least significant bits. It means the HID part always start with 0 for the first ip address. Then we can use this address as BID address. 

If we don't get the address start by 0, then we will not get required no of ipaddresses. For ex, if we start with 00001, then we end up with 100000 for getting 32 ipaddresses. This is an issue, because no of bits in HID parts are changing. So, it's mandatory for all ipaddresses in a block to start with all 0's.

Problems on CIDR
----------------
1)Given the below list of ipaddresses, findout if they form a CIDR block?<br>
10.1.2.32<br>
10.1.2.33<br>
...<br>
10.1.2.47

Ans: 
1st rule is passed -> ipaddresses are contiguous.<br>
2nd rule is passed -> no of ipaddresses(16) should be 2 power n. <br>
3rd rule is passed -> First ipaddress should be divisible by block size(16).<br>

As descirbed before, to find out if a number is divisible by 2 power n, take the least siginicant n bits. 32 in binary is 00100000. If we divide this block size(16) i.e. 10000, we get remainder as 0000. Hence this is evenly divisible.

2)Given an Classless ipaddress(10.1.2.35/27, 10.1.2.35/20), findout the address range?<br>
Ans: We know the block size is 32-27=5. Now, represent 35 in binary. i.e. 00100011. Now, replace the last 5 digits with 0's. Now you get 00100000. i.e. 32. So, the address range is from 10.1.2.32 to 10.1.2.63.

For the second question, the block size is 32-20=12. So, the Ip address for last two octets in binary form is 10.1.00000010.00100000. If we take the last 12 bits and make 0's we get the starting ip of the block. This in binary form is 10.1.00000000.00000000 which is nothing but 10.1.0.0

Subnets in CIDR
---------------
Consider an ipaddress in CIDR range 10.1.2.10/25. This means the host id part contains 7 bits. So, this CIDR block contains 128 ipaddresses. If we want to divide this into two subnets we will have two subnets with 64 ipaddresses each.

The ip 10.1.2.10 in binary form is -> 10.1.2.00001010. The starting ip for this block is 10.1.2.00000000. Now if we consider the last 7 bits and divide them into two subnets.<br> We get first subnet range from 10.1.2.00000000 to 10.1.2.00111111. <br>
The second subnet ranges from 10.1.2.01000000 to 10.1.2.0111111. 

That means ipaddress range for subnets are 10.1.2.0/26 to 10.1.2.63/26 and 10.1.2.64/26 to 10.1.2.127/26. The block id for the first subnet is 10.1.2.0/26 and 10.1.2.64/26. It became 26, because that extra 1 bit is used to identify the subnet.

Dividing the above into 4 subnets
---------------------------------
If we have to decide the above CIDR block, we need to use 2 bits to represent the subnet. The ipaddresses range in 4 subnets are 10.1.2.0/27 to 10.1.2.31/27, 10.1.2.32/27 to 10.1.2.63/27,10.1.2.64/27 to 10.1.2.95/27,10.1.2.96/27 to 10.1.2.127/27. BID size became 27 because 2 bits are used to identify subnet.

VLSM
----
Generally, ISP providers like TATA/Airtel gets these ipaddresses from IANA and allocate to companies. They generally sell different ipaddress ranges for different companies. For this VLSM is required.

Variable length subnet masking in CIDR happens the same way as in Classful ipaddresses.
For ex, 10.1.2.10/25 needs to be divided into 3 subnets, with one subnet containing 64 ipaddresses, second and third contains 32 ipaddresses each. 

For the first subnet, we need one bit to represent the subnet id. So, it's BID is 10.1.2.0/26 and range is 10.1.2.0 to 10.1.2.63.

For the second subnet, we need two bits to represent the subnet id. So, it's BID is 
10.1.2.64/27 and range is 10.1.2.64 to 10.1.2.95.

For the third subnet, we need two bits to represent the subnet id. So, it's BID is 
10.1.2.96/27 and range is 10.1.2.96 to 10.1.2.127.


