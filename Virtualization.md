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
A hypervisor is a program, firmware or hardware that adds an abstraction layer on top of the physical hardware, which si used to create virtual machines. These virtual machines than have access to all the hardware of the physical machine (CPU, memory, disk controllers and NIC).
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
The hardware is abstracted, which allows many compute instances (VMs) to share a single hosts hardware. Each VM runs with its own isolated OS.

**Containerization**
The OS is abstracted.

# Containers
## Containers are not Virtual Machines
Linux containers can be thought of as very lightweight wrappers around a single Unix process, which might spawn other processes, but one statically compiled binary can also be all that is inside a container.

Virtual machines are designed as stand-ins for real hardware and have a long(er)-lived nature than containers, which can exist for months or run a task for a minute and then be destroyed.
## Limited Isolation
Containers are isolated from one another, but the default container configuration has them all sharing CPU and memory on the host system, as they are colocated Unix processes. Unless you constrain them, containers can compete for resources.
Limits on CPU and memory use are encouraged through Docker, but are not the default.
Containers often share one or more common filesystem layers, but that means if you update a shared image, you may need to rebuild and redeploy containers that are using the older image.