# Wireshark oneliners

#### Using Wireshark locally to visualize tcpdump output from a remote server

`ssh root@dest tcpdump -u -s0 -w - 'tcp port 389' | wireshark -k -i -`
