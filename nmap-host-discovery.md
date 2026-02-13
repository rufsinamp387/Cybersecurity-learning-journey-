Nmap Host Discovery

Command Used

nmap -sn 192.168.1.1

Purpose

This command checks whether a system is alive on the network.
It does not scan ports.


nmap -sn 192.168.1.0/24 

purpose 

Scans the whole network (256 devices)
/24 = subnet range
It tells Nmap:
“Check every device from 192.168.1.0 to 192.168.1.255”


How it Works

Nmap sends a ping request to the target.
If the system responds → host is up
If no response → host is down or blocked

Example Output

Host is up (0.0020s latency)

Why Pentesters Use It

Before scanning ports, we first identify active machines.
This reduces noise and avoids scanning offline devices.

Key Learning

-sn means scan no ports
