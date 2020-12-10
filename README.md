UCLA CS118 Project (Simple Router)
====================================

For more detailed information about the project and starter code, refer to the project description on CCLE.

(For build dependencies, please refer to [`Vagrantfile`](Vagrantfile).)

## Makefile

The provided `Makefile` provides several targets, including to build `router` implementation.  The starter code includes only the framework to receive raw Ethernet frames and to send Ethernet frames to the desired interfaces.  Your job is to implement the routers logic.

Additionally, the `Makefile` a `clean` target, and `tarball` target to create the submission file as well.

You will need to modify the `Makefile` to add your userid for the `.tar.gz` turn-in at the top of the file.

## Academic Integrity Note

You must host your code in private repositories on [GitHub](https://github.com/), [GitLab](https://gitlab.com), or other places.  At the same time, you are PROHIBITED to make your code for the class project public during the class or any time after the class.  If you do so, you will be violating academic honestly policy that you have signed, as well as the student code of conduct and be subject to serious sanctions.

## Known Limitations

When POX controller is restrated, the simpler router needs to be manually stopped and started again.

## Acknowledgement

This implementation is based on the original code for Stanford CS144 lab3 (https://bitbucket.org/cs144-1617/lab3).

Name: Keano Zamora UID: 705097258

Design:
In this project, we have two components to complete. First, we are writing a simple router with a small static routing table (include a client, two servers and three interfaces). The input network should check its interface by findIfacebyName. If the interface is unknown, then drop the packet. Then it should check the ethernet header and check the eth_type field of the ethernet_hdr. There are only two types of payload type: ARP and IPv4. In the first case, if the ethernet_type is APR, we have two situations: 1. if it is a ARP Request packet, then we should prepare and send ARP response packet. 2. Else, if it is a ARP Response packet, we should record IP-MAC mapping information in the ARP cache, and we should send out all enqueued packets for ARP entry. In the second case, if the ethernet_type is IPv4, then we should verify its checksum, and if it is greater than the minimum packet size. Discard all invalid packets. If the packet is to router, we should check if the icmp_type is 8, if it is, we should response a icmp echo, otherwise, we should discard it. Then for the packet to be forwarded, we should use longest prefix match algorithm to find a next hop IP address in the routing table. Also we should lookup ARP cache for MAC address mapped to the next hop destination IP address. If it has a valid entry found: then forward packet. Else, queue receive packet and send ARP request to discover the IP-MAC mapping. simple-router: It is how the router deal with the receiving a packet on the interface. arp-cache: To send a arp request every second, if the request was sent over five times, remove it. routing-table: Using the longest-prefix match algorithm to look up a proper entry in the routing table. The final component is using a NAT for transfer a echo reply's source IP to the external interface IP and the reverse if it is a echo reply.

Issues:
First I had issues with the ARP portions of the project but piazza helped find the solution. Next, I had issues with the checksum which took awhile to debug. Also, I was confused by the wording of the NAT section of the spec. Overall I made a lot of issues throughout the project in which I had to use excessive print statements to figure out. I also want to note piazza was a lot of help as well.

