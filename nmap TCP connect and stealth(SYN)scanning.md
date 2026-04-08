TCP CONNECT SCAN


1)  nmap -sT 192.168.1.1 -p 21-5789
  
    Command Breakdown
    
    -sT: Performs a TCP Connect Scan, completing the full three-way handshake(SYN, SYN/ACK, ACK)
    
    -p 21-5789: Instructs Nmap to scan every port from 21 through 5789. 



    Expected Outcomes
    
    For each port in the range, Nmap will report one of these primary states:
    
      Open: A service is actively listening and accepted the full connection.
    
      Closed: The host responded with an RST (Reset) packet, indicating no service is listening on that port.
    
      Filtered: No response was received (or an ICMP error was returned), usually meaning a firewall is blocking the probes. 
    
    Key Considerations for this Range
    
    Scanning Time: Scanning over 5000 ports using a TCP Connect scan can be slow because each port requires a full connection attempt.
    
    Visibility: Completed connections are logged by most services and firewalls, making this scan easy to detect.
    
    Privileges: Unlike the default SYN scan (-sS), the -sT scan does not require root/sudo privileges to run.
    
    
    ![nmap4](https://github.com/user-attachments/assets/0fb49c22-9b1e-44df-a7f0-dfadfde8b930)


2) nmap -sT 192.168.1.1 -PS20-1001 


    This command is a valid Nmap scan that combines a TCP Connect Scan for port analysis with a TCP SYN Ping for host discovery. 

    Command Breakdown
   
     -sT (TCP Connect Scan): Performs a full three-way handshake to determine if ports are open. This is the standard scan type for non-root users.
    
      192.168.1.1: The target IP address.
   
     -PS20-1001 (TCP SYN Ping): Tells Nmap to use a TCP SYN packet to probe ports 20 through 1001 to see if the host is "alive" before starting the actual scan.

 STEALTH SCAN

 1) nmap -sS 192.168.1.1

    This command performs a TCP SYN scan (also known as a "half-open" or "stealth" scan) on the target. Unlike the previous -sT scan, this is the most popular and      fastest scan type in Nmap.

    
    How it Works
    
    SYN: Nmap sends a SYN (synchronize) packet to the target port.
    
    Response:
    
    SYN/ACK: The port is open. Nmap immediately sends an RST (reset) packet to close the connection before it's fully established.
    
    RST: The port is closed.
    
    No response/ICMP error: The port is filtered (likely by a firewall).

    Key Differences from your last scan
    
    Stealthier: It never completes a full TCP three-way handshake, so it’s less likely to be logged by the application layer of the target.
    
    Faster: It requires fewer packets to determine a port's status.
    
    Privileges: Unlike -sT, this command typically requires root or sudo permissions because it needs to craft raw packets.
    
    Port Range: Since you didn't specify -p, this will scan Nmap's default 1,000 most common ports rather than the 21-5789 range you used before.
    





    Nmap sends that RST (Reset) packet to keep the scan "half-open." Here are the three main reasons why:
    
      Stealth: By cutting the connection before the final ACK of the three-way handshake, Nmap avoids "completing" the session. Many older or basic logging systems       only record a connection once it is fully established. This helps the scan fly under the radar of simple application-layer logs.
    
      Speed: Completing a handshake takes time and resources. Since Nmap already knows the port is open the moment it receives a SYN/ACK, there is no reason to           waste time finishing the handshake and then sending a formal FIN to close it.
    
      Efficiency: It prevents the target from holding a "socket" open for a real session. If you were scanning thousands of ports and completing every handshake,         you could accidentally overwhelm the target's connection table (a "SYN flood" or resource exhaustion).


       
