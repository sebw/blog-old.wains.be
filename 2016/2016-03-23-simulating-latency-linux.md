# Simulating latency and other network issues on Linux

If for some reason you need to simulate latency, latency, loss, duplication or re-ordering on a linux machine, use netem (command tc)  as root 

Add a delay of 100ms on interface eth0:

    tc qdisc add dev eth0 root netem delay 100ms
    
Removing the rule is a simple:

    tc qdisc del dev eth0 root netem delay 100ms
    
Simulate packet loss:

	tc qdisc change dev eth0 root netem loss 0.1%
	
Simulate packet deduplication:

	tc qdisc change dev eth0 root netem duplicate 1%
	
Simulate packet reordering:

	tc qdisc change dev eth0 root netem delay 10ms reorder 25% 50%
    
More info: [https://wiki.linuxfoundation.org/networking/netem](https://wiki.linuxfoundation.org/networking/netem)