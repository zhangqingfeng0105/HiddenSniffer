# HiddenSniffer
ShadowRelay is a Tor routing node that is bound to one or more hidden nodes behind it. ShadowRelay actively forwards the user's traffic to the next hop or service through its hidden nodes without the user's knowledge. Not only does ShadowRelay violate the principle that only the client can choose the path, but it also reduces the anonymity and availability of the Tor network. To detect the ShadowRelays within the Tor network, we started circuit-level monitoring of nodes in the Tor network in January 2023.  

## 1 The definition of Hidden node
The hidden node is a non-Tor relay that is bound to the Tor relays and has a different IP address than the relay. The user’s traffic is forwarded to the hidden node by the Tor relay, and then forwarded by the hidden node to the next-hop relay or service. Therefore, from the perspective of the next-hop relay, the consensus IP address of the previous-hop relay is inconsistent with the source IP address of the TLS connection it established. Since relays are bound to hidden nodes, we consider relays and hidden nodes to belong to the same operator.  
(1) Tor bridge --> hidden node --> middle node  
(2) Guard node --> hidden node --> middle node  
(3) Middle node --> hidden node --> exit node  
(4) Exit node --> hidden node --> website  

## 2 ShadowRelay: Tor routing node bound to hidden nodes  
ShadowRelay is a routing node that is bound to  hidden nodes and has a hidden family relationship.

## 3 The binding method of ShadowRelay and hidden node 
The conversion of a normal Tor relay into a ShadowRelay is a relatively straightforward process. To construct a hidden node, the operator deploys a proxy forwarding process A, such as v2ray, on a separate host distinct from the Tor relay. Subsequently, the operator deploys a global proxy tool B, such as proxychains, on the host of the Tor relay, and forwards Tor traffic to proxy process A through the global proxy tool B.

## 4 Principle of the HidddenSniffer tool
HiddenSniffer is a lightweight sniffing tool designed to discover the binding relationship between ShadowRelays and hidden nodes. It is composed of a custom Tor client and a honeypot relay.  
(1) The honeypot relay is implanted into the Tor network, recording the consensus IP address of the previous hop relay and the source IP address of the TLS connection. It is worth noting that the honeypot relay functions like a normal relay, except that it is capable of recording circuit logs.  
(2) Our scanner uses the Stem library to control the client, selects the fix guard relay, the relay to be detected and the honeypot relay to create a 3-hop circuit.  
(3) The log analysis module of the honeypot relay records the previous hop relay whose consensus IP address is inconsistent with the source IP address of the TLS connection, and marks it as a potential ShadowRelay.   
