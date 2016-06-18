


date: 2008-07-23 21:23:17+00:00


# SSH local and remote port forwarding

categories:
- Linux
- Security


I use SSH local port forwarding on a daily basis but I rarely use remote port forwarding. Today I forgot about the GatewayPorts option again, so I decided to write a quick post about SSH port forwarding.

**Local port forwarding**

Accessing a service (in this example SSH port tcp/22, but it could be anything like a web server on tcp/80) on a machine at work (172.16.10.10) from your machine at home (192.168.10.10), simply by connecting to the server work.example.org at work :

`home$ ssh user@work.example.org -L 10000:172.16.10.10:22`

We see the service is available on the loopback interface only, listening on port tcp/10000 :

`home$ netstat -tunelp | grep 10000
tcp        0      0 127.0.0.1:10000         0.0.0.0:*               LISTEN      1000       71679       12468/ssh      `

From your home machine, you should be able to connect to the machine at work :

`home$ ssh root@localhost -p 10000`


**Local port forward for anyone at home !**

If you want other people on your home subnet to be able to reach the machine at work by SSH, add the option -g :

`home$ ssh user@work.example.org -L 10000:172.16.10.10:22 -g`

We now see the service is available on all interfaces on your home computer, available for anyone to connect to on the local subnet :

`home$ netstat -tunelp | grep 10000
tcp        0      0 0.0.0.0:10000           0.0.0.0:*               LISTEN      1000       72265       12543/ssh`      

Anyone on your local subnet should be able to connect to the machine at work by doing this :

`anyone$ ssh root@192.168.10.10 -p 10000`




**Remote port forwarding**

Giving access to a service (SSH port tcp/22) on your home machine (192.168.10.10) to people at work

`home$ ssh user@work.example.org -R 10000:192.168.1.10:22`

We see on our server at work (on the loopback interface on port tcp/10000) that we have access to our SSH server at home  :

`work.example.org$ netstat -tunelp | grep 10000
tcp        0      0 127.0.0.1:10000              0.0.0.0:*                   LISTEN      0          73719534   3809/1 `
        
People logged in on the machine work.example.org now should be able to SSH into your home machine by doing :

`work.example.org$ ssh user@localhost -p 10000`


**Remote port forwarding for anyone at work !**

If you want everybody on the subnet at work to be able to SSH into your home machine, there's no -g option for remote forward, so you need to change the SSH configuration of work.example.org, add to sshd_config :

`GatewayPorts yes`

Connect just as before :

`home$ ssh user@work.example.org -R 10000:192.168.1.10:22`

Now, it's listening on all interfaces on the server at work :

`work.example.org$ netstat -tunelp | grep 10000
tcp        0      0 0.0.0.0:10000                0.0.0.0:*                   LISTEN      0          73721060   4426/1`

Anyone at work can now connect to your home machine by SSH via the server :

`anyone.example.org$ ssh anyone@work.example.org -p 10000`


**Notes**

- You would need to log in as root if you want services to listen on a port < 1024.
- Don't forget to open necessary ports on any firewall either at home or work. 
- Unfortunately you can only forward services running on TCP, but there's a way to forward UDP through SSH using netcat [http://blog.wains.be/post/tunneling-udp-requests-through-ssh/](http://blog.wains.be/post/tunneling-udp-requests-through-ssh/)
