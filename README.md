*This project has been created as part of the 42 curriculum by aybelhaj.*

# NetPractice

A networking exercise project where you configure small-scale networks by solving 10 levels of increasing difficulty, covering IP addressing, subnet masks, and routing tables.

## Description

NetPractice is a system administration project from the 42 curriculum that introduces the fundamentals of **TCP/IP networking** through practical, hands-on exercises. In each level, you are given a broken network diagram that must be fixed by correctly assigning IP addresses, subnet masks, and routing information so that all devices can successfully communicate.

The project is carried out through a browser-based training interface, meaning no coding is required. The completed configurations require a deep understanding of subnetting, packet forwarding, and internet gateways.

### How to execute in Linux system
```bash
    cd net_practice
    ./run.sh
```
The NetPractice Survival Guide (Methodology)To solve the most advanced levels (Level 6 to 10), this project relies on a strict 4-step methodology:Count the Networks (Neighborhoods): Every physical connection (a wire between a host and a router, or between two routers) represents an independent network.Calculate the Masks (Subnetting): Divide larger networks into smaller blocks using CIDR notation.Assign the IPs (Neighbors): Ensure devices on the same wire share the same subnet block and mask. Two interfaces of the same router can never be on the same subnet.Build the Routing Table (The Map): Configure the forward and return paths for packets.How to Calculate Subnets (The Quick Math Method)Instead of converting IPs to binary, you can use this 3-step mathematical formula to quickly find subnet masks and IP ranges based on the CIDR notation (e.g., /26, /28, /30).Step 1: Calculate leftover host bits ($h$)Subtract the CIDR number from 32 (total IPv4 bits).h = 32 - CIDR(Example for /26: 32 - 26 = 6 bits)Step 2: Calculate the Block Size (IPs per subnet)Raise 2 to the power of the leftover bits.Block Size = 2^h(Example: 2^6 = 64 IPs per block)Step 3: Calculate the Decimal Subnet MaskSubtract the Block Size from 256.Mask = 256 - Block Size(Example: 256 - 64 = 192. So the mask is 255.255.255.192)Finding the Subnet Ranges:Simply jump by the Block Size starting from .0. For a /26 (Block of 64):Subnet 1: .0 to .63Subnet 2: .64 to .127Subnet 3: .128 to .191Subnet 4: .192 to .255Routing Logic ConceptsDefault Routes (0.0.0.0/0 or default): Used when a device only has one way out. It tells the device: "Send everything destined for unknown networks to this specific gateway." Always point hosts to their local router interface.Specific Routes (Destination Network => Next Hop IP): The Next Hop must ALWAYS be the IP of a directly connected neighbor (a router interface on the same physical wire). Routers don't have "long arms"; they can only hand packets to their immediate neighbors.Route Summarization: A technique used in Level 10. Instead of creating multiple complex routes for tiny subnets (like /28 or /30), you can use a broader mask (like /24) to group them together and route them efficiently through a single gateway.

## Project Structure
```
├── level1.json  	# Simple direct connection between two hosts
├── level2.json  	# Subnet mask matching between hosts
├── level3.json  	# Switch connecting multiple hosts
├── level4.json  	# Router connecting two networks
├── level5.json  	# Routes and default gateways
├── level6.json  	# Internet routing through a gateway
├── level7.json  	# Multiple subnets with two routers (/26 subnetting)
├── level8.json  	# Complex routing with Internet access and fixed subnets
├── level9.json  	# Four networks, two routers, Internet hacking concepts
├── level10.json 	# Final challenge — VLSM, route summarization, full topology
```
## Resources

- [IP Addressing and Subnetting](http://apuntesdenetworking.blogspot.com/2011/09/subredes-ip-ip-subnetting.html)  
- [Subnet Calculator](https://www.calculator.net/ip-subnet-calculator.html) — Useful tool for verifying subnet calculations.
- `man ip-route` — Linux routing table documentation.
- [YouTube Playlist](https://www.youtube.com/watch?v=s_Ntt6eTn94&list=PLCXqoZAc8-tzD5N5oCyIyEcMg_NDs6o7C) — Tutorials.

## AI Usage
The use of AI in this project consisted of an interactive tutoring approach. AI was used to explain abstract networking concepts, break down the mathematical formulas behind VLSM (Variable Length Subnet Masking), and help debug complex routing loops in the final levels (7 to 10) by analyzing forward/return path logs.