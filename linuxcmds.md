Find:

```
find /where/to/look/up criteria action
```

```
find /dir/path/look/up -name "dir-name-here"
```

more at: https://www.cyberciti.biz/faq/howto-find-a-directory-linux-command/


wget resume download

wget -c or --continue option to continue getting a partially downloaded file. This is useful when you want to finish a download started by a previous instance of wget, or by another program. The syntax is:

```
wget --continue url
```

Linux Firewall

Ubuntu and Debian
Issue the following command to open port 1191 for TCP traffic.
```
sudo ufw allow 1191/tcp
```
Issue the following command to open a range of ports.
```
sudo ufw allow 60000:61000/tcp
```
Issue the following command to stop and start Uncomplicated Firewall (UFW).
```
sudo ufw disable
sudo ufw enable
```

Firewall configuration using iptables

The iptables utility is available on most Linux distributions to set firewall rules and policies. These Linux distributions include Red Hat Enterprise Linux 6.8, Red Hat Enterprise Linux 7.x, CentOS 7.x, SLES 12, Ubuntu, and Debian. Before using these commands, check which firewall zones might be enabled by default. Depending upon the zone setup, the INPUT and OUTPUT terms might need to be renamed to match a zone for the desired rule. See the following Red Hat Enterprise Linux 7.x example for one such case.

Issue the following command to list the current firewall policies.
```
sudo iptables -S
sudo iptables -L
```
Issue the following command to open port 1191 (GPFS™) for inbound TCP traffic from internal subnet 172.31.1.0/24.
```
sudo iptables -A INPUT -p tcp -s 172.31.1.0/24 --dport 1191 -j ACCEPT
```
Issue the following command to open port 1191 (GPFS) for outbound TCP traffic to internal subnet 172.31.1.0/24.
```
sudo iptables -A OUTPUT -p tcp -d 172.31.1.0/24 --sport 1191 -j ACCEPT
```
Issue the following command to open port 445 (SMB) for outbound TCP traffic to external subnet 10.11.1.0/24 and only for adapter eth1.
```
sudo iptables -A OUTPUT -o eth1 -p tcp -d 10.11.1.0/24 --sport 445 -j ACCEPT
```
Issue the following command to open port 445 (SMB) for inbound TCP traffic to a range of CES IPs (10.11.1.5 through 10.11.1.11) and only for adapter eth1.
```
sudo iptables -A INPUT -i eth1 -p tcp -m iprange --dst-range 10.11.1.5-10.11.1.11 --dport 445 -j ACCEPT
```
Issue the following command to allow an internal network, eth1, to communicate with an external network, eth0.
```
sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```
Issue the following command to save firewall rule changes to persist across a reboot.
```
sudo iptables-save
```
Issue the following command to stop and start Uncomplicated Firewall (UFW).
```
service iptables stop
service iptables start
```

Forwarding internet via SSH:
(https://stackoverflow.com/questions/36353955/apt-get-install-via-tunnel-proxy-but-ssh-only-from-client-side)

Computer A

    Has access to Internet
    Has access to Computer B
    SSH is installed

Computer B

    Doesn't have access to Internet
    OpenSSH Server is installed

Steps:

    ssh into Computer B from Computer A
    ```
    sudo ssh -R <selected port>:us.archive.ubuntu.com:80 user@computerb.host
    ```

    Edit Computer B's /etc/apt/apt.conf to include the following lines:

    ```
    Acquire::http::Proxy "http://localhost:<selected port>";
    Acquire::https::Proxy "https://localhost:<selected port>";
    ```

    Run your apt-get update or install or upgrade on Computer B and it should work.

A few notes:

    You HAVE to keep the original session of ssh from Computer A to Computer B active while using Computer B to access apt-get repositories.
    You DON'T have to use the same ssh connection to utilize the tunnel (meaning if you have multiple ssh connection into Computer B, they should all work)
    
#cifs

install cifs utils:
```
apt install cifs-utils
```

Create a mount point for the shared folder
```
$ sudo mkdir /shared
```

Create a persisting cifs mount in fstab by adding the following line into /etc/fstab:
```
//SHARE_SERVER/SHARED_FOLDER /shared cifs  username=USERNAME,noauto,user 0 0
```

list processes that have NVIDIA GPU device nodes open
```
sudo fuser -v /dev/nvidia*
```

find files less than equal to 50kB
```
find ./ -mindepth 1 -maxdepth 1 -type d -exec du -ks {} + | awk '$1 <= 50' | cut -f 2-
```

find and delete files less less than equal to 50kB
```
find ./debug -mindepth 1 -maxdepth 1 -type d -exec du -ks {} + | awk '$1 <= 50' | cut -f 2- | xargs -d \\n rm -rf 
```
