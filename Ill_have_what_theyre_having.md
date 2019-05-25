have them SSH to you (I assume you're competent enough to manage your port forwarding) and forward a port back to a ssh server on their machine.

Get them to run:
```
ssh -R 48724:localhost:22 your_username@your_ip
```
You obviously might not want them logging in as your user so you could create another user and have that just for SSHing. There obviously has to be a modicum of trust between you and the other user.

And then you run:
```
ssh -p 48724 their_username@localhost
```
Using a high port so root privileges aren't required.

Of course, they'll need openssh-server installed for you to connect but that's a simple ```sudo apt-get install openssh-server```

If the server has ```GatewayPorts no```, you can reverse port tunnel by executing 
```
ssh -g -L 48725:localhost:48724 your_username@remote-machine (your_ip in this case)
```
on the server once you have executed ```ssh -R``` command on the client. 

This will make loopback port 48724 on the server accessible on all interfaces on port 48725.

The -R option tells the tunnel to answer on the remote side, which is the SSH server and the -L option tells the tunnel to answer on the local side of the tunnel, which is the host running your client.
-g Allows remote hosts to connect to local forwarded ports.

You could also add some options to your command: ssh –f –N –T –R 2210:localhost:22 username@yourMachine.com
-f: tells the SSH to background itself after it authenticates, saving you time by not having to run something on the remote server for the tunnel to remain alive.
-N: if all you need is to create a tunnel without running any remote commands then include this option to save resources.
-T: useful to disable pseudo-tty allocation, which is fitting if you are not trying to create an interactive shell.

See:
https://blog.devolutions.net/2017/3/what-is-reverse-ssh-port-forwarding
https://askubuntu.com/questions/50064/reverse-port-tunnelling
for more info