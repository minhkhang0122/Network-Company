# Network Company Design and Implementation in Cisco Packet Tracer

## Table of contents

- [Network Company Design and Implementation in Cisco Packet Tracer](#network-company-design-and-implementation-in-cisco-packet-tracer)
  - [Table of contents](#table-of-contents)
- [Overview of the Network Topology](#overview-of-the-network-topology)
- [Story](#story)
- [Requirement](#requirement)
- [Technologies Implemented](#technologies-implemented)
  - [Step 1: Adding required modules into MultiLayer Switch and Router](#step-1-adding-required-modules-into-multilayer-switch-and-router)
  - [Step 2: Adding the prerequisite device into the network topology](#step-2-adding-the-prerequisite-device-into-the-network-topology)
  - [Step 3: Configuring Switch of each department to their respective name](#step-3-configuring-switch-of-each-department-to-their-respective-name)
      - [Apply this command to all department](#apply-this-command-to-all-department)
  - [Step 4: Configure SSH to L3 Switch and Router](#step-4-configure-ssh-to-l3-switch-and-router)
  - [Step 5: Configuring access/trunk port and create VLAN](#step-5-configuring-accesstrunk-port-and-create-vlan)
        - [Do note: You need to change the VLAN of the department and cable if you connected to a different port](#do-note-you-need-to-change-the-vlan-of-the-department-and-cable-if-you-connected-to-a-different-port)
  - [Step 6: Configuring port-security for Finance department](#step-6-configuring-port-security-for-finance-department)
  - [Step 7: Subnetting IP for each flood, L3 Switch, Router, ISP](#step-7-subnetting-ip-for-each-flood-l3-switch-router-isp)
    - [First Floor](#first-floor)
    - [Second Floor](#second-floor)
    - [Third Floor](#third-floor)
    - [Router and L3 Switch Subnet](#router-and-l3-switch-subnet)
    - [Between the Routers and ISPs](#between-the-routers-and-isps)
  - [Step 8: After that we assign IP to the device](#step-8-after-that-we-assign-ip-to-the-device)
  - [Step 9: OSPF Configuration in MultiLayerSwitch, Core Router and ISP Router](#step-9-ospf-configuration-in-multilayerswitch-core-router-and-isp-router)
  - [Step 10 Assign Static IP to DHCP server, DNS Server, Server Room PC and configure DHCP, DNS](#step-10-assign-static-ip-to-dhcp-server-dns-server-server-room-pc-and-configure-dhcp-dns)
  - [Step 11 Configuring Inter-VLAN Routing(SVI) on both MultiLayerSwitch](#step-11-configuring-inter-vlan-routingsvi-on-both-multilayerswitch)
  - [Step 12 Configure Wireless AC](#step-12-configure-wireless-ac)
  - [Step 13 Configure PAT and ACL on Core Router](#step-13-configure-pat-and-acl-on-core-router)
  - [Final test Connectivity](#final-test-connectivity)

---

# Overview of the Network Topology

![alt text](/assets/overview.png)

# Story

A trading floor Support centre employs 600 staff. They have recently expanded and as a result, need to move to a new building. A building has been identified but has no network. This means that before they can move out, new network service needs to be designed and implemented in the new building. Existing Network comprises of the following elements: The new building is expected to have three floors with two departments in each for example;
- First floor- (Sales and Marketing Department-120 users expected, Human Resource and Logistics Department-120 users expected).
- Second floor- (Finance and Accounts Department-120 users expected, Administrator and Public Relations Department-120 users expected).
- Third floor- (ICT-120 users expected, Server Room-12 devices expected).


# Requirement

- Use hieratical model providing redundancy at every layer, two routers and two multilayer switches are expected to be used to provide redundancy.
- The network is also expected to connect to at least two ISPs to provide redundancy and each router to the connected to the two ISPs.
- Each department is required to have a wireless network for the users.
- Each department should be in a different VLAN and in different subnetwork.
Provided a base network of 172.16.1.0, carry out subnetting to allocate the correct number of IP addresses to each department.
- The company network is connected to the static, public IP addresses (Internet Protocol) 195.136.17.0/30, 195.136.17.4/30, 195.136.17.8/30 and 195.136.17.12/30 connected to the two Internet providers.
- Configure basic device settings such as hostnames, console password, enable password, banner messages, disable IP domain lookup.
- Devices in all the departments are required to communicate with each other with the respective multilayer switch configured for inter-VLAN routing.
- The Multilayer switches are expected to carry out both routing and switching functionalities thus will be assigned IP addresses.
- All devices in the network are expected to obtain an IP address dynamically from the dedicated DHCP servers located at the server room.
- Devices in the server room are to be allocated IP address statically.
- Use OSPF as the routing protocol to advertise routes both on the routers and multilayer switches.
- Configure SSH in all the routers and layer three switches for remote login.
- Configure port-security for the Finance and Accounts department to allow only one device to connect to a switchport, use sticky method to obtain mac-address and violation mode shutdown.
- Configure PAT to use the respective outbound router interface IPv4 address, implement the necessary ACL rule.
- Test Communication, ensure everything configured is working as expected.


# Technologies Implemented

1. Hierarchical Network Design.
2. Connecting Networking devices with Correct cabling.
3. Configuring Basic device settings.
4. Creating VLANs and assigning ports VLAN numbers.
5. Subnetting and IP Addressing.
6. Configuring Inter-VLAN Routing on the Multilayer switches (Switch Virtual Interface).
7. Configuring Dedicated DHCP Server device to provide dynamic IP allocation.
8. Configuring SSH for secure Remote access.
9. Configuring OSPF as the routing protocol.
10. Configuring NAT Overload(Port Address Translation PAT).
11. Configuring standard and extended Access Control Lists ACL.
12. Configuring switchport security or Port-Security on the switches.
13. Configuring WLAN or wireless network (Cisco Access Point).
14. Host Device Configurations.
15. Configuring ISP routers.
16. Test and Verifying Network Communication.



---

## Step 1: Adding required modules into MultiLayer Switch and Router

- Adding HWIC-2T Module so the device is Serial Cable Supported
![Serial Cable](/assets/step1_1.png)

- Adding AC-POWER-SUPPLY Module so the device can be powered on
![power supply](/assets/step1_2.png)

- Checking DCE is supported on the cable and change the clock rate to 64000
![DCE Check and change clock rate 64000](/assets/step1_3.png)

## Step 2: Adding the prerequisite device into the network topology

![Network Topology](/assets/step2_1.png)

---

## Step 3: Configuring Switch of each department to their respective name

- I configured hostname, password, disable domain lookup, banner message, console password for each Access Layer Switch

![department command](/assets/step3_1.png)
    
#### Apply this command to all department

```
enable
configure terminal
hostname [device-name]
banner motd #No Unauthorize Access#
no ip domain lookup 
line console 0
password cisco
login
exit
enable password cisco
service password-encryption 
```

---

## Step 4: Configure SSH to L3 Switch and Router

- You need to configure these 4 device SSH 

![Devices](/assets/Step4_1.png)
![Router SSH Config](/assets/step4_2.png)
![Switch SSH Config](/assets/step4_3.png)

```
enable
configure terminal
hostname [Device-Hostname]
banner motd #No Unauthorize Access#
no ip domain lookup 
line console 0
password cisco
login
exit
enable password cisco
service password-encryption 
do write
ip domain name cisco.net
username admin password cisco
crypto key generate rsa 
1024
line vty 0 15
login local
transport input ssh
exit
do write
```

---

## Step 5: Configuring access/trunk port and create VLAN 

- Only interface that connected to end-host is access port
- Interface connected to L3 Switch will be trunk port
- Configure the same command to all department 
    

![Sale Access port and Trunk Port Configuration](/assets/step5_1.png)


##### Do note: You need to change the VLAN of the department and cable if you connected to a different port
```
enable
configure terminal

int range [range of the port that connected between L3 Switch and L2 Switch]
switchport mode trunk

exit

vlan 60
name [Department-name]
vlan 99
name NotInUse
exit

int range [range of the port that connected between end-host and L2 Switch]
switchport mode access
switchport access vlan [Vlan of the department]
exit

int range g0/1-2
switchport mode access
switchport access vlan 99

exit
do write
```

![Configure trunk port for L3 Switch](/assets/step5_2.png)

- Configure the cable that connected between L3 Switch and L2 Switch
- Create VLAN for each department
```
int range [Cable that connected between L3 and L2]
switchport mode trunk
exit

vlan 10
name Sales
vlan 20
name HR
vlan 30
name Finance
vlan 40
name Admin
vlan 50
name ICT
vlan 60
name Server

exit
do write
```


---


## Step 6: Configuring port-security for Finance department

![Security Port for Finance](/assets/step6_1.png)

```
enable
configure terminal

int range [range of the port that connected to end-host through Switch]
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown 

```

---

## Step 7: Subnetting IP for each flood, L3 Switch, Router, ISP

### First Floor
<table>
    <tr>
        <th>Department</th>
        <th>Network Address</th>
        <th>Subnet Mask</th>
        <th>Host Address Range</th>
        <th>Broadcast Address</th>
    </tr>
    <tr>
        <td>
            <p>Sales & Marketing</p>
        </td>
        <td>
            <p>172.16.1.0</p>
        </td>
        <td>
            <p>255.255.255.128/25</p>
        </td>
        <td>
            <p>172.16.1.1 to 172.16.1.126</p>
        </td>
        <td>
            <p>172.16.1.127</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>HR and Logistics</p>
        </td>
        <td>
            <p>172.16.1.128</p>
        </td>
        <td>
            <p>255.255.255.128/25</p>
        </td>
        <td>
            <p>172.16.1.129 to 172.16.1.254</p>
        </td>
        <td>
            <p>172.16.1.255</p>
        </td>     
    </tr>
    
</table>

### Second Floor
<table>
    <tr>
        <th>Department</th>
        <th>Network Address</th>
        <th>Subnet Mask</th>
        <th>Host Address Range</th>
        <th>Broadcast Address</th>
    </tr>
    <tr>
        <td>
            <p>Finance & Accounts</p>
        </td>
        <td>
            <p>172.16.2.0</p>
        </td>
        <td>
            <p>255.255.255.128/25</p>
        </td>
        <td>
            <p>172.16.2.1 to 172.16.2.126</p>
        </td>
        <td>
            <p>172.16.2.127</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>Admin & Public Relations</p>
        </td>
        <td>
            <p>172.16.2.128</p>
        </td>
        <td>
            <p>255.255.255.128/25</p>
        </td>
        <td>
            <p>172.16.2.129 to 172.16.2.254</p>
        </td>
        <td>
            <p>172.16.2.255</p>
        </td>     
    </tr>
    
</table>

### Third Floor
<table>
    <tr>
        <th>Department</th>
        <th>Network Address</th>
        <th>Subnet Mask</th>
        <th>Host Address Range</th>
        <th>Broadcast Address</th>
    </tr>
    <tr>
        <td>
            <p>ICT</p>
        </td>
        <td>
            <p>172.16.3.0</p>
        </td>
        <td>
            <p>255.255.255.128/25</p>
        </td>
        <td>
            <p>172.16.3.1 to 172.16.3.126</p>
        </td>
        <td>
            <p>172.16.3.127</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>Server Room</p>
        </td>
        <td>
            <p>172.16.3.128</p>
        </td>
        <td>
            <p>255.255.255.252/28</p>
        </td>
        <td>
            <p>172.16.3.129 to 172.16.3.142</p>
        </td>
        <td>
            <p>172.16.3.143</p>
        </td>     
    </tr>
    
</table>

### Router and L3 Switch Subnet
<table>
    <tr>
        <th>No</th>
        <th>Network Address</th>
        <th>Subnet Mask</th>
        <th>Host Address Range</th>
        <th>Broadcast Address</th>
    </tr>
    <tr>
        <td>
            <p>R1-MLSW1</p>
        </td>
        <td>
            <p>172.16.3.144/30</p>
        </td>
        <td>
            <p>255.255.255.252</p>
        </td>
        <td>
            <p>172.16.3.145 to 172.16.3.146</p>
        </td>
        <td>
            <p>172.16.3.147</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>R1-MLSW2</p>
        </td>
        <td>
            <p>172.16.3.148/30</p>
        </td>
        <td>
            <p>255.255.255.252</p>
        </td>
        <td>
            <p>172.16.3.149 to 172.16.3.150</p>
        </td>
        <td>
            <p>172.16.3.151</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>R2-MLSW1</p>
        </td>
        <td>
            <p>172.16.3.152/30</p>
        </td>
        <td>
            <p>255.255.255.252</p>
        </td>
        <td>
            <p>172.16.3.153 to 172.16.3.154</p>
        </td>
        <td>
            <p>172.16.3.155</p>
        </td>     
    </tr>
    <tr>
        <td>
            <p>R2-MLSW2</p>
        </td>
        <td>
            <p>172.16.3.156/30</p>
        </td>
        <td>
            <p>255.255.255.252</p>
        </td>
        <td>
            <p>172.16.3.157 to 172.16.3.158</p>
        </td>
        <td>
            <p>172.16.3.159</p>
        </td>     
    </tr>
    
</table>

### Between the Routers and ISPs
- Public IP addresses 195.136.17.0/30, 195.136.17.4/30, 195.136.17.8/30 and 195.136.17.12/30


## Step 8: After that we assign IP to the device
![Assigning IP address](/assets/step8_1.png)


---


## Step 9: OSPF Configuration in MultiLayerSwitch, Core Router and ISP Router
![MultiLayerSwitch1](/assets/MultiLayerSW1OSPF.png)
![MultiLayerSwitch2](/assets/MultiLayerSW2OSPF.png)
![Router 1](/assets/RouterOSPF.png)
![Router 2](/assets/Router2OSPF.png)

```
For both Switch
ip routing 
router ospf 10
router-id [x.x.x.x]
network 172.16.1.0 0.0.0.127 area 0
network 172.16.1.128 0.0.0.127 area 0
network 172.16.2.0 0.0.0.127 area 0
network 172.16.2.128 0.0.0.127 area 0
network 172.16.3.0 0.0.0.127 area 0
network 172.16.3.0 0.0.0.15 area 0

-> Do note that you need to change these 2 IP
network 172.16.3.xxx 0.0.0.3 area 0
network 172.16.3.xxx 0.0.0.3 area 0
```

```
router ospf 10
router-id [x.x.x.x]

network 172.16.3.144 0.0.0.3 area 0
network 172.16.3.152 0.0.0.3 area 0

-> Chang these 2 IP aswell
network 195.136.xx.xx 0.0.0.3 area 0
network 195.136.xx.xx 0.0.0.3 area 0
```

## Step 10 Assign Static IP to DHCP server, DNS Server, Server Room PC and configure DHCP, DNS
- Configure Static IP on DHCP Server, DNS Server, Server Room PC
![DCHP](/assets/Step10_DCHP.png)
![SV PC](/assets/Step10_SVPC.png)
![DNS](/assets/Step10_DNS.png)

- After this we will configure DHCP to automatically assign IPs to end-host
![DHCP Pool configure](/assets/Step10_DHCPPool.png)
![DNS server name](/assets/Step10_DNSDomain.png)
  
## Step 11 Configuring Inter-VLAN Routing(SVI) on both MultiLayerSwitch
- Before doing this, you must have each department VLAN in the VLAN table
- Using 'show ip vlan brief' => To see if you have any VLAN configured
- If not, the VLAN interface will not run

![SVI Configuring](/assets/Step11_SVI.png)

```
int vlan 10
ip address 172.16.1.1 255.255.255.128
ip helper-address 172.16.3.130

int vlan 20
ip address 172.16.1.129 255.255.255.128
ip helper-address 172.16.3.130
no shut
exit

int vlan 30
ip address 172.16.2.1 255.255.255.128
ip helper-address 172.16.3.130
no shut
exit

int vlan 40
ip address 172.16.2.129 255.255.255.128
ip helper-address 172.16.3.130
no shut
exit

int vlan 50
ip address 172.16.3.1 255.255.255.128
ip helper-address 172.16.3.130
no shut
exit

int vlan 60
ip address 172.16.3.129 255.255.255.240
ip helper-address 172.16.3.130
no shut
exit
```

## Step 12 Configure Wireless AC
- If you do not remember how to configure Wireless AC click this [link](https://github.com/minhkhang0122/SOHO)
![alt text](/assets/Step12_AC.png)

## Step 13 Configure PAT and ACL on Core Router
![NAT configure Router 1](/assets/Step13_NAT.png)
![NAT configure Router 2](/assets/Step13_ACLNAT.png)
```
ip nat inside source list 1 int se0/2/0 overload
ip nat inside source list 1 int se0/2/1 overload
access-list 1 permit 172.16.1.0 0.0.0.127
access-list 1 permit 172.16.1.128 0.0.0.127
access-list 1 permit 172.16.2.0 0.0.0.127
access-list 1 permit 172.16.2.128 0.0.0.127
access-list 1 permit 172.16.3.0 0.0.0.127
access-list 1 permit 172.16.3.128 0.0.0.15
int range g0/0-1
ip nat inside 
int s0/2/1
ip nat outside
int s0/2/0
ip nat outside
```

```

```

- After finishing configuring NAT you must configure Static Route to Core Router and MultiLayer Switch

```
-> This is for both MultilayerSwitch
-> Cable may vary
ip route 0.0.0.0 0.0.0.0 g1/0/1
ip route 0.0.0.0 0.0.0.0 g1/0/2 70


-> This is for both Core Router
-> Cable may vary
ip route 0.0.0.0 0.0.0.0 s0/2/0
ip route 0.0.0.0 0.0.0.0 s0/2/1 70
```

## Final test Connectivity
- Ping from different department
- Use SSH to access Router
- Ping over the Internet and NAT Translation table
![Department](/assets/department.png)
![SSH](/assets/SSH.png)
![Ping over the Internet](/assets/Ping%20over%20NAT.png)
![NAT table](/assets/NATtable.png)