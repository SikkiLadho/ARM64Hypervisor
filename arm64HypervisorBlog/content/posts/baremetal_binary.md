---
title: "Baremetal Hypervisor Binary"
date: 2022-04-25T22:20:55+05:00
draft: true
---

You must be bored of reading a lot of theory, don't worry, we'll be writing actual code on an actual hardware. First of all, we will need the startup code, which sets up everything for us. In the startup code we will:
- make sure that only primary core executes the startup code, while other four cores should hang in a loop.(RPI4 has four cores, one is primary, other 3 cores are called secondary cores.)
- set stack pointer for the primary
- clear the bss section. BSS section is a section in memory for uninitialized variables.
- jump to the main function in C!

Following are the contents are **boot.S**, our startup code.

```

#include "mm.h"

.section ".text.boot"

.globl _start
_start:
// get the core id of current core.
	mrs	x0, mpidr_el1
	and	x0, x0,#0xFF
// jump to master label, if core id is zero or we are on the primary core!
	cbz	x0, master
	b	proc_hang


// hang in a loop if we are on the secondary core
proc_hang:
	b 	proc_hang


// primary cpu jumps here
master:

	// get the address for bss_begin section(defined in linker.)
	adr	x0, bss_begin
	// get the address for bss_end section(defined in the linker script.)
	adr	x1, bss_end

	sub	x1, x1, x0
	bl 	memzero

// set stack pointer
	mov	sp, #LOW_MEMORY
// jump to hypervisor
	bl	hyp_main
	b 	proc_hang		// should never come here
```

Here's the contents of **memzero.S**, which contains the memzero asm function.

```
.globl memzero
memzero:
	str xzr, [x0], #8
	subs x1, x1, #8
	b.gt memzero
	ret
```

Here's the contents of hypervisor.c, where our main function decides.

```
void kernel_main(void)
{

	return;
}
```


Here's the contents of linker.ld, which links all the files and defines different sections for the whole binary.

```


```

Here's the Makefile, which makes it easy to compile everything.



### How would you compile and
