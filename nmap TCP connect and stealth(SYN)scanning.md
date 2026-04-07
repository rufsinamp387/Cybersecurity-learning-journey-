nmap -sT 192.168.1.1 -p 21-5789

Command Breakdown

-sT: Performs a TCP Connect Scan, completing the full three-way handshake.

-p 21-5789: Instructs Nmap to scan every port from 21 through 5789. 


Key Considerations for this Range

Scanning Time: Scanning over 5000 ports using a TCP Connect scan can be slow because each port requires a full connection attempt.

Visibility: Completed connections are logged by most services and firewalls, making this scan easy to detect.

Privileges: Unlike the default SYN scan (-sS), the -sT scan does not require root/sudo privileges to run.


![nmap4](https://github.com/user-attachments/assets/0fb49c22-9b1e-44df-a7f0-dfadfde8b930)
