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


1) nmap -sT 192.168.1.1 -PS20-1001 


    This command is a valid Nmap scan that combines a TCP Connect Scan for port analysis with a TCP SYN Ping for host discovery. 

    Command Breakdown
   
     -sT (TCP Connect Scan): Performs a full three-way handshake to determine if ports are open. This is the standard scan type for non-root users.
    
      192.168.1.1: The target IP address.
   
     -PS20-1001 (TCP SYN Ping): Tells Nmap to use a TCP SYN packet to probe ports 20 through 1001 to see if the host is "alive" before starting the actual scan.


   How This Command Executes
   
   Host Discovery Phase: Nmap sends SYN packets to the range 20–1001. If any port in that range responds (with a SYN/ACK or RST), Nmap considers the host "up".
   Port Scanning Phase: Once confirmed "up," Nmap performs a full TCP Connect scan on the default 1,000 most common ports. 
 
