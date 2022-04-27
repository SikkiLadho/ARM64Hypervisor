---

title: "Tutorial 1: Exception Levels"
author: "Mushahid Hussain(SikkiLadho)"
categories: ["tutorial", "hypervisor"]
date: "2022-04-25"


---

Today, we will be learning about exception levels.(have patience, we'll write actual code too, but in the next post.)
Exceptions levels define execution privilege at each level. There are 4 exception levels in ARMv8 architecture.

 - **Exception Level 0 (EL0)**: This Exception Level or Privilege Level is commonly used by userspace applications. Firefox, Libreoffice, VLC Media Player, and VirtualBox are a few examples of userspace applications.
 - **Exception Level 1 (EL1)**: Kernel and all privileged code associated with kernel works in EL1 execution level.
 - **Exception Level 2 (EL2)**: Hypervisor(including KVM) works in exception level.
 - **Exception Level 3 (EL3)**: Secure Monitor

You might be wondering how we go from one exception level to another. **Exception** is any event that can cause the currently executing program to be suspended and cause a state change to execute code to handle that exception. Other processor architectures might describe this as an interrupt. Exception Levels would remain the same or increase when an exception occurs. Exceptions would always be handled at the same exception level or higher.

Let's understand this with a simple example. Imagine that you have developed an operating system kernel running at EL1 and you want to wake up a secondary CPU core(it is asleep at the start.). The code which makes it possible to wake up a secondary core is present at EL3 in the form of an **exception handler**. You would cause an exception to occur and EL3 would wake up the core for you. When the handler at EL3 does its magic, it would then return to your exception level.


Following instructions can cause different exceptions to occur. (Assuming that hypervisor is not trapping exceptions, we'll know more about SMC trapping in future posts.)

- `SMC` or **Secure Monitor Call** instruction in armv8 assembly can cause an exception to occur, which will normally be handled at EL3 or Secure Monitor.
- `hvc` or **Hypervisor Call** is another instruction that can cause an exception, to be handled at EL2 or Hypervisor.
- `svc` or **Supervisor Call** instruction can cause an exception to occur, which will be handled at EL0 or Kernel.



Note that exceptions would increase either the exception level or the exception level would remain the same. The occurrence of an exception would never decrease the exception level. Conversely, returning from an exception would always cause the exception level to decrease or remain the same.

- `eret` instruction can be used to return to a lower exception level or remain on the same exception level. When an exception handler does what it has done, then it will end the exception by using the `eret` instruction.


I hope you were able to digest everything. Please refer to [this documentation](https://developer.arm.com/documentation/den0024/a), if you would like to know more. That is one of the excellent documentation I have seen. That is it for today. Now those basics are covered, we will try to write a bare-metal hypervisor binary at EL2 or Hypervisor Level!. Stay Tuned.
