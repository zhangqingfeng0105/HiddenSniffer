We will update the data collected using the HiddenSniffer tool every month. The data set has 11 fields.  

-----------------------------------------------------------------------------------------------------  
id:  data index  
cell_command:  cell_command in the data cell, where constant equals 10, means CREATE CELL  
p_circ_id:  our honeypot relay displays the circuit ID of the routing node to be detected, such as A --p_circ_id--> honepot relay      
p_chan_addr:  the IP address of hidden node  
canonical_addr:  the IP address of ShadowRelay in our honeypot relay's cache as queried by the node identifier in CREATE CELL   
consensus_addr:  the IP address of ShadowRelay in the consensus file.  
fingerprint:  the fingerprint of ShadowRelay.  
p_flags:  the flag of ShadowRelay.  
p_bandwidth:  the consensus bandwidth of ShadowRelay.  
is_tor_node:  whether p_chan_addr appears in the latest consensus file? if yes, is_tor_node=1. Otherwise, is_tor_node=0  
record_time:  detection time 
