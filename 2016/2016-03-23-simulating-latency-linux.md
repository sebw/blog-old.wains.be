# Simulating latency on Linux

If for some reason you need to simulate latency on a linux machine, use this as root (expected that the interface is eth0 and the delay 100ms):

    tc qdisc add dev eth0 root netem delay 100ms
    
Removing the rule is a simple

    tc qdisc del dev eth0 root netem delay 100ms