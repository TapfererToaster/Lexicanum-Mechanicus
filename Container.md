Containers are built around encapsulating and creating standardized software units, packaging an applications code and its dependencies such that they can be deployed in any environment with expected, repeatable and consistent results.

Container are lightweight, small in size, utilize fewer resources and have quicker boot times then VMs which have a lot of overhead. 

# Characteristics
## Containers are not Virtual Machines
Linux containers can be thought of as very lightweight wrappers around a single Unix process, which might spawn other processes, but one statically compiled binary can also be all that is inside a container.

Virtual machines are designed as stand-ins for real hardware and have a long(er)-lived nature than containers, which can exist for months or run a task for a minute and then be destroyed.
## Limited Isolation
Containers are isolated from one another, but the default container configuration has them all sharing CPU and memory on the host system, as they are colocated Unix processes. Unless you constrain them, containers can compete for resources.
Limits on CPU and memory use are encouraged through Docker, but are not the default.
Containers often share one or more common filesystem layers, but that means if you update a shared image, you may need to rebuild and redeploy containers that are using the older image.
## Lightweight
Containers are small, a newly created container takes only 12 kilobytes of disk space.