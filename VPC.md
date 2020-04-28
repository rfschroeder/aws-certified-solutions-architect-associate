# Virtual Private Cloud
## Introduction
## Build a Custom VPC
## Network Address Translation (NAT)
## Access Control Lists (ACL)
## Custom VPC and ELBs
## VPC Flow Logs
## Bastions
## Direct Connect
## Setting Up a VPN Over a Direct Connect Connection
## Global Accelerator
## VPC End Points
## Summary

We cannot route traffic to a __NAT gateway__ or __VPC gateway__ endpoints through a __VPC peering__ connection, a __VPN connection__, or __AWS Direct Connect__. A NAT gateway or VPC gateway endpoints cannot be used by resources on the other side of these connections. Conversely, a NAT gateway // VPC gateway endpoints cannot send traffic over VPC endpoints, AWS VPN connections, Direct Connect or VPC Peering connections either.

Every route table contains a __local route__ for communication within the VPC over IPv4. We __cannot modify or delete__ these routes.

__VPC Endpoints always take precedence__ over NAT Gateways or Internet Gateways. 

Network ACL __rules are evaluated in order__, starting with the lowest numbered rule. As soon as a rule matches, it is applied regardless of any higher numbered rule that may contradict it.

SSH connections are between port 22 of the host and __an ephemeral port of the client__. In fact, this is true for any TCP service.

Security groups are __stateful__, this means any connection initiated successfully will be completed.

We can create __S3 proxy server__ for enabling use cases where S3 has to be accessed privately through VPN connection, AWS Direct Connect or VPC peering.

AWS __reserves 5 IPs for every subnet__, not for every VPC.

Instances in __custom VPCs don't get public DNS hosts by default__, we have to set the `enableDnsHostnames` attribute to true. The `enableDnsSupport` is to be set to true too, but that is done by default.

We can set a __custom route table as the main route table__.

We can add __secondary CIDR ranges__ to an existing VPC. When a secondary CIDR block is added to a VPC, a route for that block with target as "local" is automatically added to the route table.

__VPC peering__ connection route contains Target as `pcx-xxxxxx`.
__VPN connection__ // __Direct Connect__ connection route contains Target as `vgw-xxxxxx`.

__VPN__ is established over a __Virtual Private Gateway__.

AWS __VPC Endpoints support S3 and DynamoDB__. For __Amazon ECR__, we have to use __AWS PrivateLink__.

__Difference between DirectConnect and VPN__ — DirectConnect does not involve the Internet, while VPN does.

__AWS Direct Connect__ doesn't __encrypt in transit data__, while __VPN__ does.

To establish a __VPN connection__, we need —
- A public IP address on the customer gateway for the on-premise network.
- A virtual private gateway attached to the VPC.

To setup __AWS VPN CloudHub__ —

- Each regional site should have non overlapping IP prefixes.
- BGP ASN should be unique at each site.
- If BGP ASN are not unique, additional ALLOW-INs will be required.

The __allowed block size__ in VPC is between a /16 netmask (65,536 IP addresses) and /28 netmask (16 IP addresses).

 The following __VPC peering connection configurations__ are __not supported__ —

1. Overlapping CIDR Blocks
2. Transitive Peering
3. Edge to Edge Routing Through a Gateway or Private Connection

We can move part of our __on-premise address space to AWS__. This is called BYOIP. For this, we have to acquire a __ROA, Root Origin Authorization__ from the the regional internet registry and submit it to Amazon.

