---

title: "Tutorial: Exception Levels"
author: "Mushahid Hussain(SikkiLadho)"
categories: ["tutorial", "hypervisor"]

---


Exceptions levels define execution privelege at each level. There are 4 exception levels in ARMv8 architecture. 

 - **Exception Level 0 (EL0)**: This Exception Level or Privelege Level is commonly used by userspace applications. Firefox, Libreoffice, VLC Media Player, VirtualBox are few examples of userspace applications. 
 - **Exception Level 1 (EL1)**: Kernel and all privileged code associated with kernel works in EL1 execution level. 
 - **Exception Level 2 (EL2)**: Hypervisor(including KVM) works in exception level.
 - **Exception Level 3 (EL3)**: Secure Monitor

That is it.



