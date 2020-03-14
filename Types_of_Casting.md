Any packet sent over network contains 3 parts. <br>
a)Data<br>
b)Source address<br>
c)Destination address

For example a host with ipaddress 12.2.3.2 wants to send a message to another ipaddress 24.1.2.2. Any packet sent will be of the format

		[data]|[12.2.3.2]|[24.1.2.2]

The ip address of the source computer nework is 12.0.0.0. Generally, the network ipaddress starts with 0's. Similarly, for the destination ipaddress, the network ipaddress is 24.0.0.0.


Unicast
-------
Sending a packet from one host to another host is called UniCasting.

Broadcast
---------
Sending a packet from one host to multple hosts is called Broadcasting. Broadcasting is of two types.<br>

a)Limited broadcasting --> A message is sent to all other hosts in the same network.
In a Class A ipaddress range, if source wants to send a packet to all hosts in the network, it needs to send 16M packets. This is practically impossible. So, in Limited broadcasting a source uses the destination ipaddress in the packet as 255.255.255.255, so that it will be sent to all hosts in the network. Packet format is:

		[data]|[12.2.3.2]|[12.255.255.255]

Note: The ip address 255.255.255.255 should not be used in any network, because this represent Limited broadcast address(LBA).

b)Directed broadcasting --> If you want send a message from a source to all hosts in the destination network, we use Directed broadcasting. The packet format is 

		[data]|[12.2.3.2]|[24.255.255.255]
	
Note: Network ipaddress ends with all 0's, where as Directed broadcast address end with all 1's. So, even though there 2^n, ipaddresses are present in any network, 2 addresses are reserved for network ipaddress and directed broadcast address(DBA).

Questions
----------
Findout the NID,LBA and DBA for the below ipaddresses.

|Ip address	| Class   |Network ID |Limited Broadcast Address|Directed Broadcast Address	|
|---------------|:--------:|:----------|:---------------|:--------------|
|1.2.3.4 	 	|A         |1.0.0.0    |255.255.255.255	|1.255.255.255	|
|10.15.20.60	|A         |10.0.0.0   |255.255.255.255	|10.255.255.255 |
|130.1.2.3      |B         |130.1.0.0  |255.255.255.255	|130.255.255.255|
|150.0.150.150  |B         |150.0.0.0  |255.255.255.255	|150.0.255.255  | 
|200.1.10.10    |C         |200.1.10.0 |255.255.255.255	|200.1.10.255   |
|220.15.1.10    |C         |200.15.1.10|255.255.255.255	|220.15.1.255	|
|250.0.1.2	    |E         |N/A  	   |N/A				|N/A			|
|300.0.1.2	    |Invalid IP|N/A  	   |N/A				|N/A			|

	



