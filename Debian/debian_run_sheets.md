

**Run Sheet: Securing a Debian-Based System with iptables**

**1. Connect to the System:**
   - Log in to the Debian-based system with administrative or superuser privileges.

**2. Prioritize Critical Tasks:**
   - Before proceeding, prioritize the following critical tasks:
     - Ensure you have reliable backups in place.
     - Change passwords.
     - Create a superuser.
     - Set up a basic firewall using `iptables`.
     - Configure a static ARP entry.
     - List all accounts.
     - List all superusers.
     - Disable any unnecessary or compromised accounts.
     - Clear scheduled tasks for all users.
     - Review and compare the sources list to official repositories to check for tampering.
     - Run system updates.

**3. Change Passwords:**
   - Change passwords for all accounts with weak or compromised passwords:
  
   sudo passwd <username>


**4. Create a Super User:**
   - Create a superuser or administrator account if one doesn't already exist:
  
  
   sudo adduser <newadmin>


**5. Set Up a Basic iptables Firewall:**
   - Configure a basic `iptables` firewall to restrict incoming and outgoing traffic, allowing only necessary services:

   
   # Flush existing rules
   iptables -F
   iptables -X
   iptables -Z

   # Set default policies to DROP
   iptables -P INPUT DROP
   iptables -P FORWARD DROP
   iptables -P OUTPUT DROP

   # Allow loopback traffic
   iptables -A INPUT -i lo -j ACCEPT
   iptables -A OUTPUT -o lo -j ACCEPT

   # Allow established and related connections
   iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

   # Allow SSH on port 22 (if needed)
   iptables -A INPUT -p tcp --dport 22 -j ACCEPT

   # Allow specific ports (any hosted service port, HTTP on port 80, and HTTPS on port 443)
   iptables -A INPUT -p tcp --dport 80 -j ACCEPT
   iptables -A INPUT -p tcp --dport 443 -j ACCEPT

   # Save iptables rules
   service iptables save

   # Start and enable iptables service
   systemctl start iptables
   systemctl enable iptables
 

**6. Configure a Static ARP Entry:**
   - To configure a static ARP entry, use the `arp` command. Replace `<ip_address>` and `<mac_address>` with the actual IP and MAC addresses:


   sudo arp -s <ip_address> <mac_address>


**7. List All Accounts:**
   - List all user accounts on the system:
  

   cut -d: -f1 /etc/passwd


**8. List All Super Users:**
   - List all users with superuser privileges:
  

   grep -E 'root|sudo' /etc/group


**9. Disable Unnecessary or Compromised Accounts:**
   - Disable any unnecessary or compromised user accounts:
  
  
   sudo passwd -l <username>


**10. Clear Scheduled Tasks for All Users:**
    - Clear scheduled tasks for all users, including potential malicious tasks:
    

    sudo crontab -r


**11. Compare Sources List to Official Repositories:**
    - Review and compare the `/etc/apt/sources.list` file with official Debian repositories to check for tampering. If any discrepancies are found, correct them to ensure you're using trusted sources.

   - Official Debian Repository sources:


   deb http://deb.debian.org/debian/ bullseye main
   deb-src http://deb.debian.org/debian/ bullseye main
   deb http://security.debian.org/debian-security/ bullseye/updates main
   deb-src http://security.debian.org/debian-security/ bullseye/updates main


   Then, import the Debian GPG key:

 
   sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com $(wget -qO - https://packages.debian.org/stable/all/apt-transport-https/download | dpkg-deb --fsys-tarfile /dev/stdin | tar -xO ./usr/share/keyrings/debian-archive-keyring.gpg)
   ```
**12. Run System Updates:**
   - Update the system packages and software to patch known vulnerabilities:

   
   sudo apt update
   sudo apt upgrade
  

**13. Test Firewall and System:**
    - Test the system's functionality and connectivity to ensure that it allows necessary traffic while blocking unauthorized access.

**14. Continuously Monitor and Improve:**
    - Establish a monitoring and incident response process to continuously assess and enhance the security of your Debian-based system.
```

