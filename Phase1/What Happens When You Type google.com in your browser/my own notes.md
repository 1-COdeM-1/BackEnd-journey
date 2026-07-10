Understanding Web Requests: A Deep Dive
1. The DNS Resolution (Finding the Destination)
What is it? The "Internet Phonebook." It translates human-readable domain names (e.g., google.com) into machine-readable IP addresses.

The Process:

Browser Cache: Checks if it knows the IP already.

OS Cache: Checks gethostbyname and the hosts file.

DNS Server: If not found locally, it queries a configured DNS server (like your ISP or Google DNS).

Security Note: Standard DNS is unencrypted, meaning "Middlemen" (ISPs, attackers) can see which domains you visit. Technologies like DoH (DNS over HTTPS) are used to encrypt these queries.

2. The ARP Protocol (The Local Communicator)
What is it? The protocol used to map a known IP Address to a physical MAC Address within a local network (LAN).

When does it happen? Every time your device needs to send data to another device on the same local subnet (like sending a request to your Router to reach the internet).

How it works: Your device broadcasts an ARP Request: "Who has IP 192.168.1.1? Tell me your MAC address." The owner responds with its MAC Address.

Key takeaway: IP addresses are for "Global Routing," while MAC addresses are for "Local Delivery."

3. The Request Lifecycle (From Browser to Server)
Step 1 (DNS): Convert google.com to an IP.

Step 2 (ARP): Find the MAC address of your Gateway (Router) to exit your local network.

Step 3 (The Travel): Your data packet travels through various routers. At every "hop" (station), the router uses ARP to find the next device's MAC address to pass the packet along.

Step 4 (Arrival): The packet reaches the target server's IP address (The "Airport").

Step 5 (Delivery): The server's Web Server (e.g., Nginx) receives the request. It looks at the HTTP Host Header (e.g., Host: google.com) to decide which internal service or application should handle the request.

4. Crucial Concepts for Backend Engineers
Anycast & Load Balancing: A single domain (like google.com) doesn't have one fixed IP; it maps to many servers based on geography and traffic.

Virtual Hosting: One physical server (one IP) can host multiple websites/apps. The Host Header is what differentiates the traffic.

Hard-coded IPs: Never hard-code an IP in your production code. Always rely on Domain Names, as IP addresses are dynamic and can change.
