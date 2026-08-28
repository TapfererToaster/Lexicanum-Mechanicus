[Cisco Networking Academy](https://www.netacad.com/launch?id=75cbc2e3-bab4-484c-a925-ad839c127c20&tab=curriculum&view=4c5c0198-806d-5896-a0af-65b1e4fe4ac8)
# Different Approaches to hosting
![[Traditional vs virtualization vs containerisation.png]]

**Traditional approach**
Applications are installed on an OS, which is directly installed on the hardware. Having multiple applications on the one server, often lead to resource starvation or conflicts with processes and libraries (Dynamic Link Libraries (DLL) hell).
The solution to this problem was to host each application on its own physical server. This introduces problems; you needed multiple physical server, which would need more rack space, which needed more floor space, cabling, power, cooling, etc. Additionally if you had over-resourced and under-utilized servers, it would cost a lot of money and had very little output. 

**Virtualization approach**
Through virtualization you can use multiple [[Virtual Machines]] on a single physical server, which means that you can run multiple applications on a single server, resulting in greater resource utilization, less floor space, power and cooling as well as fewer cost to deliver the same output as the traditional approach.

**Containerization approach**
With [[Container]] you no longer need to provide a OS for each apps, resulting in even fewer costs to deliver output, as well as greater resource utilization, efficiency, smaller sizes, faster boot-up and more.
  
# Hypervisors
A hypervisor is a program, firmware or hardware that adds an abstraction layer on top of the physical hardware, which is used to create virtual machines. These virtual machines than have access to all the hardware of the physical machine (CPU, memory, disk controllers and NIC).
There are two types of hypervisors:
- **Bare Metal** 
  These hypervisors are installed directly on the hardware and than instances of operating systems are installed on the hypervisor.
  These are usually used on enterprise servers and data centers.
- **Hosted Hypervisor** 
  A hosted hypervisor is installed on top of an existing OS and then additional OS instances are installed on top of the hypervisor.

Virtualization is used in [[Virtual Machines]] and [[Container]].

# Abstraction
*Abstraction* is the basis for virtualization, the machine that is used to achieve abstraction is a hypervisor.
Abstraction means to remove dependencies and filtering out characteristics that are not relevant, in this case it is the hardware, resulting in that the VM is no longer dependent of the hardware.

>[!note] Virtualisation vs Containerisation
>*Containerisation* is about the abstraction at the OS level, while *virtualisation* is about the abstraction at the hardware level.

# Virtualization vs. Containerisation
**Virtualization**
The hardware is abstracted, which allows multiple compute instances (VMs) to share a single hosts hardware. Each VM runs with its own isolated OS. 
Der Zugriff der VMs auf die Hardwarekomponenten des Hosts wird dabei durch Konfigurationseinstellungen und Treiber gesteuert.


**Containerization** / **Anwendungsvirtualisierung**
Bei einer virtualisierten Anwendung wird diese nicht im Betriebssystem eines Computers registriert, sondern erhält eine isolierte Umgebung in de sie mit minimalen Rechten ausgeführt wird. 

# Network Functions Virtualization (NFV)
*Network functions virtualization (NFV)* refers to VMs that operate as network devices (router, firewall, load balancer, intrusion detection system, etc.), which are traditionally deployed as hardware. 
## Virtual Switching
Virtual switches are software-based switches that reside in the hypervisor kernel and provide network connectivity between VMs/containers and the node, which connects to external networks, but also executes functions such as MAC learning, link aggregation and more. 
Virtual switches allow to rapidly create new network functions in software.
>[!note]
>Common virtual switches are: 
>- VMware vSwitch
>- Microsoft Hyper-V Virtual Switch
>- a Linux bridge
>- Open vSwitch (OVS)

## Network Virtualization
Network virtualization can be achieved by using an overlay-based protocol such as *Virtual Extensible LAN (VXLAN)* to build connectivity between hypervisor-based virtual switches.
This creates Layer 2 connectivity and tunneling between VMs that run on different physical hosts independent of the physical network. This means that the physical network could be Layer 2, Layer 3 or a combination.

>[!note] Underlay and Overlay Network
>- *Underlay Network*: the physical network that you physically cable up
>- *Overlay Network*: virtualized network that dynamically creates tunnels between virtual switches 

Network virtualization solutions use a centralized control plane to distribute the mapping information between the overlay and underlay networks. This centralized approach limits the scalability, interoperability and flexibility, which gives way to alternatives like *Ethernet VPN (EVPN)*. EVPN is a distributed protocol, in which every network device distributes the mapping information (via *Border Gateway Protocol (BGP)*) to the rest of the network to establish VXLAN tunnels.