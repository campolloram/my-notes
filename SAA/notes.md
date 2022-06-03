# AWS Accounts

- Having multiple accounts (one for dev, one for test another one for prod) can limit the damage if some information is leaked, since they are containers and only the resources of that account can be deleted.


## Setting up basic AWS Account config
- In real world usage, under account settings, fill the alternate contacts list to keep the owners of the accourn on the loop.

- Activate the IAM access to billing information under settings  as well. This way you don't need to be signed in with your root user to see the information.



## MFA (Multi Factor Authentication)

A factor is a piece of evidence that provides an identity

The 4 most common factors are:
1. Knowledge -> Username and passwords
2. Possession -> Bank Card, MFA device (token generator, could be Gmail)
3. Inherent -> Fingerprint, voice, etc.
4. Location -> A network or WIFI


### How to secure an AWS account with MFA?
1. Go to the right top menu and select "security credentials"
2. Go to MFA and select an option (the easiest one is Virtual MFA)
3. Use any third party application to set up the MFA on your mobile phone or PC (google authenticator is the easiest one)


**You should set a different MFA for each user in the account**


## Budgets
### Setting up budget alerts
1. Go to the right top menu and select "billing dashboard"
2. Go to Billing Preferences and check "Receive invoce by email", "Receive Free tier alert" and "receive billing alerts"

### Creating budget
1. In the billing dashboard go to "Budgets" and "Create a new Budget"
    - Enable the cost explorer
2. Create a Cost Budget
    - Monthly, Recurrent, Fixed & the amount you want
3. Create a budget alert between 50%-80%


# IAM (Identity and Access Management)
**It is globally recilient (stored in all the world)**

There are two different types of users in AWS. You are either the account owner (root user) or you are an AWS  IAM user. The only restrictions from IAM compared to the root user is on some billing features and account closure.

### IAM lets you create 3 different types of identity objects:
1. Users -> Humans or applications that need access to your account
2. Groups -> Collection of related users (development team, finance, HR)
3. Roles -> Can be used by AWS Services or to grant external access to your account

The difference between users and roles is that a user is attached to a specific application or human and the role is like a blueprint you can use for any number of services (like a bunch of EC2 instances or an external application trying to use an S3 bucket)


Policies -> Allow or Deny access to AWS Services ONLY WHEN THEY ARE ATTACHED TO ANY OF THE 3 OBJECTS ABOVE


### In general IAM does:

1. Manages Identities - AN ID Provider (IDP)
2. Authenticate
3. Authorize


**You can create an account alias for a friendlier interface**
go to IAM -> left menu you should see a create alias button


### Creating an admin user
go to IAM -> User -> Create new user -> Attach existing policy for AdministratorAccess.


### Access Keys

An IAM user can have 2 access keys at most.

They can be created and deleted or made active or inactive

Access keys are formed by 2 parts:

1. Access Key (similart to a username)
2. Secret Access Key (similar to a password)

You only get the Secret Access Key ID one time, its your responsibility to store it somewhere.


Rotating access keys just means to create a new pair and remove the old one (that's why you can have 2 of them at the same time). update your applications to use that one instead.


### AWS CLI

use

```
aws configure --profile name_of_profile
```
to confgure multiple AWS accounts credentials in your machine.


# Cloud Computing Fundamentals

Characteristics for a system to be considered cloud

1. On-Demand Self-Service
2. Broad Netweork Access
3. Resource Pooling
4. Rapid Elasticity
5. Measured Service


### On-Demand Self-Service
can provision capabilities as needed without requiring human interaction, on demand.


### Broad Network Access
Capabilites are available over the netowork and access through standard mechanisms

### Resource Pooling
No control or knowledge over the EXACT location of the resources.

Resources are pooled to server multiple consumers using a multi-tenant model.

### Rapid Elasticity
Capabilities can be elastically provisioned and released to scale rapidly outward and inward with deman.

To the consumer, the capabilities available for provisioning often appear to be unlimited.

### Measured Service

Resources usage can be monitored, controlled, reported AND billed.



## Public vs Private vs Hybrid vs Multi Cloud

### Public Cloud
Considered public because they meet the 5 essential characteristics listed above AND because its open to the general public.


### Private Cloud on-premises
Using a service from a vendor within premises, this allows 0 latency (usually needed when delaing with huge amount of data processing.) It still needs to meet the 5 cloud characteristics. e.g. (AWS outposts, Azure Stack and Google Anthos)


### Multi Cloud
Using multiple cloud environments (hosting in AWS, Azure, Google Cloud, etc.), this way you are resilient to a vendor.


###  Hbyrid Cloud
Using private and public cloud together.


**NOTE: Having a public cloud + legacy on premises environment, this is called a HBYRID ENVIRONMENT/NETWORK**

## Cloud as a Service [X as a Service] e.g. SaaS

### Infrastructure/Application Stack
A collection of things that a software needs stacked from the botton.

In a stack there are parts that you manage and parts that are managed by your vendor.

**Unit of consumption** - What you consume in a service. Can be a service like Netflix or a service like EC2 instance.

### Infrastructure as a Service (IaaS) e.g. EC2
You pay a fee by time (minute, hour, etc.) and your vendor takes care of everything up to the O/S level. Starting from there is your responsibility to implement the remaining things.

### Platform as a Service (PaaS) e.g. Hosting an app in Heroku or using Beanstalk
Your unit of consumption is the runtime of a runtime environment (python, javascript, etc.)
This is mainly used by developers.

### Software as a Service (SaaS) e.g. Gmail, Dropbox
You consume the application. You pay a monthly fee for it.


![As a service](../media/SaaS.png)



# Tech Fundamentals
## YAML
Design to serialize data in a human readable way

Is commonly used for configuration.
Supports lists & dictionaries e.g.

![YAML example](../media/YAML_example.png)


## Networking
OSI 7- Layer Model (Networking Stack)

![OSI Model](../media/OSI_model.png)

### Layer 1 (Physical Layer)

If using a shared medium (a HUB) this HUB retransmitt everything that it receives to all of the devices connected. Including Errors and collisions

It's like shouting to a room with other people and not using any names


![OSI layer 1 hub](../media/OSI_layer_1_network.png)

![OSI layer 1 recap](../media/OSI_layer_1_key_points.png)



### Layer 2 (Data Link) e.g. Ethernet
It runs over layer 1

Introduces the concept of Frames (Ethernet frame), which are a format for sending information over a layer 2 network

It introduces MAC address for every device in the network, this address IS NOT software assigned, it is a unique addresses attached to a specific piece of hardware.
It is divided in two parts:

1. Organizational Unique Identifier - (OUI) this one is regarding the producer of the hardware 
2. Network Interface Controller (NIC)

This two parts together is what makes the address unique.


**Frame**
It is a protocolized way of transmitting data used by layer 3. It contains information about the MAC source, MAC destination and the Ether Type (e.g. IP addresses)
It also contains the payload which is between 45-1500 bytes.

**NOTE** When there is no destination MAC address (all Fs) it is known as broadcasting.

![OSI layer 2 Frame](../media/OSI_layer_2_frame.png)


Layer 2 checks for a carrier to see if another MAC address is transmitting, if a carrier is detected it waits for it to finish, this way there is no collision of data.

Using a Switch over a HUB is better since it understands layer 2 (hast layer 2 software inside of it) (has a MAC Address table), this means that can avoid collisions


![OSI layer 2 Switch](../media/OSI_layer_2_switch.png)
![OSI layer 2 Recap](../media/OSI_layer_2_recap.png)


### Layer 3 - Network (IP protocol) (Routers)
The purpose of this layer is to get data from one location to another.

Data are moved in packets (similar to Frames), this contains data to be moved as well as a destination and source addresses.

![OSI layer 3 IP Packets](../media/OSI_layer_3_IP_packets.png)


**IPv4**

AP addresses are separated into two parts the NETWORK identifier and the HOST identifier. To know if two devices are local, you just need to see if both networks are the same.

**A subnet mask is used to identify the network on an IP address**

for example a /16 submask means that the first 2 bytes of the IP is the HOST.

e.g.

133.33.3.7/16

means that the network start is

133.33.0.0

and the network end is 

133.33.255.255

This is used for machines to know when they need to route packets accross different intermediate tables (different hosts) or just to your local LAN.


**Route Tables and Routes**

This table are used by Internet providers to forward your requests to the correct destination. If there are multiple matches it uses the more specifc one. /0 is the least specific /32 is the most specific (it actually is a single IPv4 address since it has all 4 bytes)

If there are no matches it uses the default destination 0.0.0.0/0


**Address Resolution Protocol (ARP)**
When you want to encapsulate an IP Packet into a Frame for a given MAC Address, but you don't know the MAC address of the gateway, that's when you use ARP, this will give you that MAC Address.

This protocol broadcasts in layer 2 asking which device has a certain IP, the device that has that IP responds to the broadcast.


![OSI layer 3 Recap](../media/OSI_layer_3_recap.png)


### Layer 4 - Transport (maybe layer 5)

This layer helps to order IP packets.
It also helps to distinguish between applications, since layer 3 does not offer any way to distinguish between two or more connections.

IT introduces two protocols - TCP & UDP

**TCP** - Transmission Control Protocol -This is used for reliability and it is used for HTTP, HTTPS, SSH, etc.
It is a connection oriented protocol, this means you need to set up a connection between the two devices and it creates a bi-directional channel of communication.

**UDP** - User Datagram Protocol - This protocol is less realiable since it does not need the overhead of TCP, but it also has a better performance due to this.


**TCP continuation**

It uses segments which are encapsulated within IP packets.
A segement contains the SOURCE and DESTINATION PORTS. This gives us the ability to have multiple communications to a single IP e.g. TCP port 433 is HTTPS. 

It also contains a SEQUENCE NUMBER, this sequence number contians the order of the packets. This way the evice knows for which segment the IP packet belongs to and also in which order it should go.


The ACKNOWLEDGMENT field is used for letting know the source that it received the package

WINDOW - this field is used for letting the source know how many bytes you can receive between acknowledgement. Once you reach that window, the source pauses until you acknowledge the packages receives. The larger the window the faster the connection since you need less headers.

CHECKSUM - this field is used for error checking and retransmission of data



![OSI layer 4 TCP Segments](../media/OSI_layer_4_tcp_segment.png)


The Ephemeral port is the port of the client connecting to the server, and the well known port is the port of the server (433 for HTTPS)

![OSI layer 4 TCP Segments](../media/OSI_layer_4_tcp_connection.png)


The TCP 3-way Handshake

It is used for setting up the connection

first the client needs to inform the server the sequence number. It has the SYN flag set and sends it to the server.

Now that the server knows the sequence number, it creates a segment with the flag SYN-ACK to inform the client that it received the package and also sends its own sequence number and the client sequence number + 1

(sequence number are initialized to a random number for security reasons)

![OSI layer 4 TCP 3 way handshake](../media/OSI_layer_4_tcp_3_way_handshake.png)


**Firewalls**

Stateless Firewall - It needs both an Outbound rule and Inbound rule. This firewall in AWS is the - Network ACL -


Stateful Firewall - This understands the state of the TCP segment, so if you  allow the initial connection you automatically allow the response. This in AWS is called a Security Group. (This may be considered layer 5 since it knows the session, meaning the on going communication)


### Network Address Translation (NAT)

Is designed to overcome the IPv4 shortages.

It translate private IP addresses to public IP addresses


**Static NAT** - Translate from 1 private to 1 fixed public address. This is called as an Internet Gateway in AWS (IGW)
![Static NAT](../media/static_NAT.png)

**Dynamic NAT** - Translate 1 private to 1st available Public IP.

![Dynamic NAT](../media/dynamic_NAT.png)


**Port Address Translation (PAT)** many private to 1 public (NATGW) This is used by your home internet router. This method uses ports to help identify the devices.
![PAT NAT](../media/PAT_NAT.png)

ALL OF THIS IS ONLY FOR IPv4 for IPv6 is not necessary since there are plenty of IPs for all devices.


### IPv4 Addressing
![IPv4 Key Points](../media/IPv4_addressing_key_points.png)

![IPv4 classes](../media/IPv4_IP_classes.png)

Basically Class A IPs support less networks (only 256) but waaay much more hosts, since each network has 16+ million IPs. They are were used by large companies, and all the classes that follow have the same principle (networks get bigger, but hosts get smaller since they won't probably use that much hosting)
**Private Ranges**

![IPv4 classes](../media/IPv4_private_ips.png)


**IPv4 vs IPv6**

![IPv4 vs IPv6](../media/IPv4_vs_IPv6.png)



### IPv4 Subnetting
This is breaking a big network into smaller networks by using a subnet.

![IPv4 classes](../media/IP_subnetting.png)



### DDoS
These attacks are used to deny the service of your applications to any user by overloading your website.


There are 3 main types of DDoS attacks:
1. Application - Uses botnets to request really expensive endpoints
2. Protocol - Uses botnets to attempt to initiate a TCP connection with your servers (3 way handshake) but they use a spoof IP so that the server response never reaches anything and it keeps waiting for a long time.
3. Volumetric - Smaller botnets, they use different DNS servers to send requests using your IP as the source addresss. This makes the DNS servers respond to your website and overloads it.


### SSL and TLS
Gives privacy anmd data integrity between client & server.

TLS - encrypts communications
Identity (server or client/server)

verified, usually the client verifies the server.

Ensures a reliable connection, protects alteration of data in transit.


TLS works as follow:
1. First the client sends a hello message containing the information about the TLS version, supported cipher suites, session ids, etc.
2. The server responds with an agreement of the cipher suite, etc. As well as its certificate published by an CA (Certificate Authority).
3. The client validates the certificate by posting to the CA for checking expiration dates, DNS, etc.
4. If the certification is valid, the client uses the server public key to encrypt a message containing the PRE-MASTER KEY.
5. The server decrypts the pre-master key using its private key and both the client and the server generate the master key, this master key is used for doing symmetric encryption.

![IPv4 classes](../media/SSL_TLS.png)




# AWS Fundamentals
AWS services can be categorized into 2 main types
1. Public Services
2. Private Services


This public or private means to the networking only

A public service is something accessed via public endpoints e.g. S3

A private service is something accessed only via the V.P.C


Permissions control the access to a public service and networking manages the access to private service


V.P.C is proportional to your home network, it can only be accessed if you allow it and configure it.


There are 3 different network zones
1. Public internet
2. AWS private zone
3. AWS public zone


You could connect private networks directly to a private zone service, or you could use an internet GateWay to connect you private zone to the public internet.


![IPv4 classes](../media/AWS_types_of_networks.png)

