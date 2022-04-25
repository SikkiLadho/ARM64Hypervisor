---

title: "Tutorial: Exception Levels"
author: "Mushahid Hussain(SikkiLadho)"
categories: ["tutorial", "hypervisor"]

---

Today, we try to write a simple bootable hypervisor binary with just a blank screen(have patience, we'll make it print the hello world too, but in future).
Exceptions levels define execution privelege at each level. There are 4 exception levels in ARMv8 architecture.

 - **Exception Level 0 (EL0)**: This Exception Level or Privelege Level is commonly used by userspace applications. Firefox, Libreoffice, VLC Media Player, VirtualBox are few examples of userspace applications.
 - **Exception Level 1 (EL1)**: Kernel and all privileged code associated with kernel works in EL1 execution level.
 - **Exception Level 2 (EL2)**: Hypervisor(including KVM) works in exception level.
 - **Exception Level 3 (EL3)**: Secure Monitor

You might be wondering how we go from one exception level to another. **Exception** is any event that can cause the currently executing program to be suspended and cause a change in state to execute code to handle that exception. Other processor architectures might describe this as an interrupt. Exception Level would remain the same of increase, when an exception occurs. Exceptions would always be handled at the same exception level or a higher.

Let's understand this with a simple example. Imagine that you have developed an operating system kernel running at EL1 and you want wake up a secondary cpu core(it is asleep at the start.). The code which makes it possible to wake up a secondary core, is present at EL3 in the form of an **exception handler**. You would cause an exception to occur and EL3 would wake up the core for you. When handler at EL3 does its magic, it would then return to your exception level.


Following instructions can cause different exceptions to occur. (Assuming that hypervisor is not trapping exceptions, we'll know more about smc trapping in future posts.)

- `smc` or **Secure Monitor Call** instruction in armv8 assembly can cause an exception to occur, which will normally be handled at EL3 or Secure Monitor.
- `hvc` or **Hypervisor Call** is another instruction which can cause an exception, to be handled at EL2 or Hypervisor.
- `svc` or **Supervisor Call** instruction can cause an exception to occur, which will be handled at EL0 or Kernel.



Note that exceptions would increase either the exception level or the exception level would remain same. Occurance of an exception would never decrease the exception level. Convversly, returing from an exception would always cause the exception level to decrease or remain same.

- `eret` instruction can be used to return to a lower exception level or remain on the same exception level. When an exception handler does what it has do, then it will end the exception by using `eret` instruction.


I hope you were able to digest everything. Please refer to [this documentation](https://developer.arm.com/documentation/den0024/a), if you would like to know more. That is one of the excellent documentations I have seen. That is it for today. Now that basics are covered, we will try to write the a bare metal hypervisor binary at EL2 or Hypervisor Level!. Stay Tuned.
