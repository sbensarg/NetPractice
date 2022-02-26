# NetPractice


# Theorique

### Network mask
The network mask is used to determine which portion of the IP address is the network address and which is the host address.

### Classful vs. Classless Masking
- Classful refers to the network classes of A, B and C represented by the dot decimal format like 255.255.255.0 
The latest and greatest network methodology is called classless networks where class networks are subnetted into smaller subnets.
 A new method of representing the subnet mask was created to provide a better representation: the subnet mask prefix. For example, /24 

### Route table
A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed.
Each route in a table specifies a destination and a target. For example, to enable your subnet to access the internet through an internet gateway, add the following route to your subnet route table. The destination for the route is 0.0.0.0/0, which represents all IPv4 addresses. The target is the internet gateway that's attached to your VPC.
Destination	Target
0.0.0.0/0	igw-id
### Gateway
A gateway is the entrance point to another network.
A default gateway is the address to which packets are sent if there is no specific gateway for a given destination listed in the routing table.
### Router
A router is a device that connects two or more packet-switched networks or subnetworks. 
### Switch
A network switch connects devices (such as computers, printers, wireless access points) in a network to each other
#### Level 1

Here we need to set up computers within the same home network.
Initially, the connection does not work because the computer has

Interface B1
IP : 104.39.23.12
Mask : 255.255.255.0

It follows that
Network:  104.39.23.0

Diaposon: 104.39.23.1 - 104.39.23.254

And at Computer A1 104.93.23.17 What is not included in this range.

Therefore, we change the IP of A1 to a suitable one from the range and voila ... Similarly with the second computer

#### Level 2

It is very similar to the first task, only here, in order for computers to communicate with each other, they must be within the same network.

To understand which network, take the mask from A1 and IP from B1 and calculate which network

IP : 192.168.20.222
Mask : 255.255.255.224

It turns out

Network:  192.168.20.192
Diaposon: 192.168.20.193 - 192.168.20.222

To make it work, we take any IP from the range and put it in A1, and also change the mask from B1 to the same A1
Goal 2:
Computers C1 and D1 cannot communicate because the range 127.0.0.1 - 127.255.255.254 is used to communicate with itself (Addresses on Loopback)
To solve this problem, we simply take a different address space

#### Level 3
Here we have a new object. Network switch (slang. switch, switch from the English. switch - switch) - a device designed to connect several nodes of a computer network within one or more network segments.
It is very important that the switch works within the same network
Similarly to the previous tasks, we take the mask from C1 and IP from A1 and build a suitable network
It turns out

Network:  104.198.133.0
Diaposon: 104.198.133.1 - 104.198.133.126

Next, just fill in any IP from the range and do not forget about the masks :)

#### Level 4
A new Router object is added here.

In this task, we need to Connect two clients to each other and also each client with a router, 3 interfaces for connecting to a router are available for us
In order for everything to work, we need both clients and the router interface to be all within the same network (we take an empty interface and select the appropriate IP and mask for it, such that it includes client A1)

#### Level 5
Here we have a new graph, let's see what it is
    client A: Machine A
    Routes :
    ... => ...
This thing is called a static route.
A static route is used when a computer wants to reach someone outside of its network.
If the destination matches the left side (0.0.0.0/0 in this example, which is "default", which means it matches everything), it will ask the right side (192.168.0.254 here) to forward the message

The "right side" is called the gateway, on your own computer (your ISP router): every time you want to go online, your computer asks it because it's the only one that knows where to go.
First, you need to set up the "correct network" :

Here is an example of how it works

1) We sort of figured it out with you a little, let's try to solve our problem, specify the static route to whom we will send (to everyone: 0.0.0.0/0), and through which interface (18.171.197.126)
2) Also, interface A1 and R1 must be in the same network (we already know how to do this :). )
3) Also, the B1 and R2 interfaces must be on the same network (we already know how to do this :). )
4) And finally, we need to set up a static route for B (set the right parameter, the path through the R2 interface

#### Level 6

Here we have to set up internet connection
1) First, let's set up the interaction of the A1 and R1 interfaces in the same network (we already did this with you)
2) Next, in router R on the left, we specify what we send to all networks
3) Well, the last thing in internet I indicate what we will send to our network (83.71.194.129/25)

#### Level 7

Here we need to configure everything so that two computers communicate with each other using two routers
It is important here that there is no intersection of networks
A) Make interface A1 and interface R11 the same subnet mask
To set up client A, go to Interface A1 -> Interface R11.
(B) R12 interface and R21 interface must have the same subnet mask.
In the configuration of roter R1, set the value Interface R12 -> Interface R21.
In the R2 rotor configuration, configure Interface R21 -> Interface R12.
(C) R22 interface and C1 interface must have the same subnet mask.
In client C configuration, configure Interface C1 -> Interface R22.
(A), (B) and (C) each have different subnet masks
Because the router connects to a different network, the IP address on the same network is displayed

#### Level 8

Internet routes populate the network address of the network connected to the interface connected to the Internet
Private IP addresses cannot be used if they are connected to the Internet
10.0.0.0 ~ 10.255.255.255 (10.0.0.0/8) (Class A)
172.16.0.0 ~ 172.31.255.255 (172.16.0.0/12) (Class B)
192.168.0.0 ~ 192.168.255.255 (192.168.0.0/16) (Class C)
1) Set up internet I so that it sends requests through Interface R12
2) Now in Interface R13 we specify the network and mask, the same through which router R2 sends
3) Now in Interface R21 we specify the network with which Interface R13 is connected
4) Now in router R1 we specify that the packets go through the Interface R21 interface
5) Now you need to divide Interface R23 and Interface R22 into two subnets 30.12.23.1 and 30.12.23.17
6) Now we need to configure client D and client C to work with our interfaces
7) Now you need to configure Interface D1 and Interface C1 so that they are on the same network with Interface R23 and Interface R22.
