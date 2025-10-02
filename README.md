# Ex. No: 9 - Packet Tracer: Subnet an IPv4 Network
## Date: 27-09-2025
## Name: Santhosh K
## RegNo: 212223100050

## Objective
Design, configure, and verify an IPv4 subnetting scheme in Cisco Packet Tracer.<br>
•	Subnet the 192.168.0.0/24 network into multiple subnets.<br>
•	Assign addresses to LAN-A, LAN-B, and future networks.<br>
•	Configure IP addressing on routers, switches, and PCs.<br>
•	Verify connectivity using ping and router show commands.<br>

## Apparatus / Tools Required
•	Cisco Packet Tracer<br>
•	CustomerRouter (2911 or equivalent)<br>
•	ISP Router<br>
•	2 Customer Switches (LAN-A Switch, LAN-B Switch)<br>
•	ISP Switch<br>
•	2 PCs (PC-A, PC-B)<br>
•	ISP Workstation and ISP Server<br>
•	Copper straight-through cables for LAN links<br>
•	Serial DCE/DTE cable for WAN link<br>
<br>

## Network Topology Diagram

<img width="831" height="268" alt="image" src="https://github.com/user-attachments/assets/6b54bfb0-5937-43bf-83d9-4feb25c4c9c3" />

<br>

## Addressing Table

| Subnet     | Network ID   | First Usable Address | Last Usable Address | Broadcast Address | Prefix | Subnet Mask     | 
|------------|--------------|----------------------|---------------------|-------------------|--------|-----------------|
| **LAN-A**  | 192.168.0.0  | 192.168.0.1          | 192.168.0.62        | 192.168.0.63      | /26    |255.255.255.192  |
| **LAN-B**  | 192.168.0.64 | 192.168.0.65         | 192.168.0.126       | 192.168.0.127     | /26    |255.255.255.192  |

| Device         |	Interface |	IP Address                                |	Subnet Mask	    | Default Gateway     |
| ---------------|------------|-------------------------------------------|-----------------|---------------------|
| **CustomerRouter** | G0/0	      | 192.168.0.1 (1st host of LAN-A subnet)    |	255.255.255.192	| N/A                 |
| **CustomerRouter** | G0/1       |	192.168.0.65 (1st host of LAN-B subnet)   | 255.255.255.192 |	N/A                 |
| **CustomerRouter** | S0/1/0     |	209.165.201.2                             |	255.255.255.252 |	N/A                 |
| **LAN-A Switch**   | VLAN1      |	192.168.0.2 (2nd host of LAN-A subnet)    |	255.255.255.192 |	CustomerRouter G0/0 |
| **LAN-B Switch**	 | VLAN1      |	192.168.0.66 (2nd host of LAN-B subnet)   |	255.255.255.192 |	CustomerRouter G0/1 |
| **PC-A**           | NIC        |	192.168.0.62 (Last host of LAN-A subnet)  |	255.255.255.192 |	CustomerRouter G0/0 |
| **PC-B**           | NIC        |	192.168.0.126(Last host of LAN-B subnet)  |	255.255.255.192 |	CustomerRouter G0/1 |
| **ISP Router**     | G0/0       |	209.165.200.225                           |	255.255.255.224 |	N/A                 |
| **ISP Router**     | S0/1/0     |	209.165.201.1                             |	255.255.255.252 |	N/A                 |
| **ISP Switch**     | VLAN1      |	209.165.200.226                           |	255.255.255.224	| 209.165.200.225     |
| **ISP Workstation** |	NIC       |	209.165.200.235                           |	255.255.255.224 |	209.165.200.225     |
| *ISP Server**     |	NIC       |	209.165.200.240                           |	255.255.255.224 |	209.165.200.225     |

(LAN-A and LAN-B IPs to be filled with subnetting calculation.)

<br>

## Procedure
### Part 1: Subnet the Assigned Network
1.	Start with 192.168.0.0/24.<br>
2.	Requirements:<br>
o	LAN-A: ≥50 hosts<br>
o	LAN-B: ≥40 hosts<br>
o	At least 2 unused subnets for future expansion.<br>
3.	Choose a subnet mask that supports both host requirements.<br>
o	Example: /26 (255.255.255.192) → 62 hosts per subnet, 4 subnets.
4.	Allocate:<br>
o	Subnet 1 → LAN-A<br>
o	Subnet 2 → LAN-B<br>
o	Subnets 3 & 4 → Reserved<br>
<br>

### Part 2: Configure the Devices
#### CustomerRoute:r<br>
1.  Set hostname: hostname CustomerRouter<br>
2.  Passwords:<br>
o	enable secret Class123<br>
o	line console 0 → password Cisco123 → login<br>
#### Configure interfaces:<br>
•	 interface g0/0  <br>
•	 ip address 192.168.0.1  255.255.255.0
•	 no shutdown  
•	interface g0/1  
•	 ip address 192.168.0.64 255.255.255.0  <br>
•	 no shutdown  <br>
•	interface s0/1/0  <br>
•	 ip address 209.165.201.2 255.255.255.252  <br>
•	 clock rate 64000   ← DCE end  <br>
•	 no shutdown  <br>
•	Save: copy running-config startup-configv
#### Switches (LAN-A, LAN-B)<br>
•	VLAN1 IP: 2nd host of subnet  (192.168.0.2, 192.168.0.65)<br>
•	Default gateway: Router G0/0 or G0/1<br>
#### PCs (PC-A, PC-B)<br>
•	Last host of subnets(192.168.0.62, 192.168.0.126<br>
•	Subnet mask(255.255.255.192) and gateway configured(192.168.0.1, 192.168.0.65)<br>
<br>
### Part 3: Verification & Testing
1.	On routers:<br>
o	show ip interface brief (check status up/up)<br>
o	show ip route (verify connected subnets)<br>
2.	On PCs:<br>
o	Ping default gateway<br>
o	Ping across subnets (PC-A ↔ PC-B)<br>
o	Ping ISP Server<br>
<br>

## Commands Used (Summary)
•	Mode/navigation: enable, configure terminal, end<br>
•	Interface config: interface g0/0, ip address, no shutdown<br>
•	Show/verify: show ip interface brief, show ip route<br>
•	Save: copy running-config startup-config<br>
<br>

## Output (Attach Screenshots)

### Successful Completion Status

<img width="649" height="509" alt="Screenshot 2025-10-02 194301" src="https://github.com/user-attachments/assets/1108d179-c79a-4fbf-94dd-0ea1d868dd6e" />
<br>

<img width="1920" height="1080" alt="Screenshot 2025-10-02 194317" src="https://github.com/user-attachments/assets/9e22bf3d-9fd7-463f-abcf-5b439527cb62" />



### •	show ip interface brief on CustomerRouter<br>

<img width="877" height="889" alt="Screenshot 2025-10-02 193438" src="https://github.com/user-attachments/assets/9ae452eb-d78a-4330-a906-958605141b37" />

### •	show ip route<br>

<img width="793" height="333" alt="Screenshot 2025-10-02 193551" src="https://github.com/user-attachments/assets/dc6689c3-fd0d-4dd8-a7a5-08f11c7565ae" />

### •	Successful pings: PC-A → PC-B, PC-A → ISP Server<br>

#### PC-A → PC-B
<img width="877" height="889" alt="Screenshot 2025-10-02 193648" src="https://github.com/user-attachments/assets/11f39685-a7e1-4411-af78-e9179b3f1c85" />

#### PC-A → ISP Server
<img width="877" height="889" alt="Screenshot 2025-10-02 194012" src="https://github.com/user-attachments/assets/9b1f7457-1678-4cfb-91ae-a57757e00399" />


<br>

## Result
The IPv4 subnetting scheme was successfully designed and implemented. Router, switches, and PCs were configured with correct addressing. Connectivity within LANs, across subnets, and to ISP devices was verified using ping and show commands.<br>
