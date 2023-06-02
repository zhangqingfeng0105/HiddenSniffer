# HiddenSniffer
To detect the ShadowRelays within the Tor network, we started circuit-level monitoring of nodes in the Tor network in January 2023, which will help us filter out hidden nodes in the Tor network.  

1 The definition of Hidden node
It is a host with a separate IP and can forward traffic from the Tor routing node to the next-hop routing node or destination. Most importantly, it is not exposed in the consensus file. It has the following forms,  
(1) Tor bridge --> hidden node --> middle node  
(2) Guard node --> hidden node --> middle node  
(3) Middle node --> hidden node --> exit node  
(4) Exit node --> hidden node --> website  

2 ShadowRelay: Tor routing node bound to hidden nodes  
