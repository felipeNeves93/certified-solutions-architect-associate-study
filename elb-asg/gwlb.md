****
**Gateway Load Balancer**

* Deploy, scale and manage a fleet of 3rd party network virtual appliances in AWS
* Examples: 
  * Firewalls
  * Intrusion Detection
  * Prevention Systems
  * Deep Packet Inspection Systems
  * Payload Manipulation
* Operates at Layer 3 (Network-Layer) - IP Packets
* Combines the following functions:
  * **Transparent Network Gateway** - Single entry/exit for all traffic
  * **Load Balancer** - Distributes traffic to your virtual applicances
* Uses the **GENEVE** protocol on port **6081**

**Target Groups**

* **EC2 Instances**
* **IP Addresses** - Must be private IPs