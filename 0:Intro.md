---

title: "Day 0: Introduction"

date: 2022-04-16T23:24:05+05:00

---
# 0: Introduction
This is a series of tutorials that I never had a year ago when I decided to write a bare metal hypervisor on Raspberry Pi 4. I did not have prior experience with bare-metal or even kernel development. Therefore, I will be sharing all that I have learned in following series of tutorials. You are welcome to contribute to this project and I would also love to learn from you. I'm really excited that we're on this journey together.

## What is a hypervisor?

Hypervisor is a software which creates and runs virtual machines. There can two types of hypervisors. They can be classified into two categories: Type 1 or bare metal and Type 2. 

 - **Type 1:** Type 1, also known as bare metal hypervisors, have direct access to the hardware and controls all the operating systems that are running on the system.  Xen and Hyper-V are bare metal hypervisors.
 - **Type 2:** Type, also know as hosted hypervisors have to go through the host operating system to reach the hardware. An example of Type 2 hypervisor is VirtualBox.
 
 ## What would be the scope?
 Bare metal hypervisors can be very complex. Therefore, we would limit our scope at first. We will be gradually writing a simple hypervisor, which can write to serial console, successfully load a Linux kernel, trap exceptions or smc calls and manage stage 2 memory management. Our hypervisor would only run a single virtual machine. Probably after accomplishing these milestones, we can go further. I will be writing a post at most every week and we'll write this hypervisor together.
## Hardware prerequisites
 - An RPi4 with a dedicated power supply
 - A micro-SD card to boot the RPi4 from
 - A computer with a GNU/Linux distribution on it.
 - UART to TTL cable
 
 ## Software prerequisites
You will need a GNU/Linux distribution on your laptop/desktop. Please install one if you do not have it. GNU/Linux operating systems are open-source, free(as in freedom of speech as well as in free beer) and lightweight.

You should be able to flash the SD card with Raspbian, raspberry pi's recommended operating system. For now, we only need this.  

We will also use Trusted Firmware-A(TF-A) as the firmware implementation for raspberry Pi 4. You can follow [these instructions](https://trustedfirmware-a.readthedocs.io/en/latest/plat/rpi4.html) to compile and use it in your Raspberry Pi. 

You will be using UART serial console to debug your hypervisor. Therefore, you'll need to learn to use a serial console with raspberry pi. Don't worry, Adafruit has [great tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable/overview) on it.

For now this is all we need. In the next post, we will be able to boot a hypervisor binary.  
