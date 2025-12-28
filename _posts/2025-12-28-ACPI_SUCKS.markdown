---
layout: post
title:  "ACPI SUCKS"
date:   2025-12-28
categories: rants
---

NOTE: I only have a small part of ACPI 1.0 implemented (some parsing and helper functions, just the FACP currently), so please comment and give me any knowledge you may know of it in case I am wrong about anything!

## My opinion on ACPI

I personally highly dislike ACPI but after some work its pretty easy to implement once you are willing to read hundreds of pages of documentation. I mostly dislike it because of one specific thing, how much memory and paging stuff you need to mess with, I mean seriously, everything you want to do, you need to search for its header in the RSDT, from there you need you unmap the header of the thing you just searched for, map the entire thing after you have its physical memory address, usually you identity map it, and then from here you setup a bunch of extra stuff, and finally, you parse the table, if its encoded in AML you need to pass it through your AML interpreter, and you see why its a mess now, don`t you?

## Why we are stuck with ACPI

Its a standard, and one used by intel at that, we will be stuck with it until we make a better, less cluttered and messy standard, but most of these issues were fixed with ACPI 2.0+, right, RIGHT?

### ACPI 2.0+ STILL SUCKS

ACPI 2.0+ Is more clean, provides more things, but guess what, it is 64bit, and does a bunch of big messy stuff, and you know what that means? The same mess from before, but you need to use different things, instead of the RSDP you have the XSDP, instead of the RSDT, XSDT, because they wanted to use 64bit pointers, which means we are stuck with 2 versions of the RSDP and XSDP and almost everything else, including a bunch of ACPI 2.0+ only features, making even more issues, and now, we are stuck, with having to try to do a bunch of extra stuff to figure out what version of ACPI is running on your system.
Why ACPI is kinda nice still

ACPI, while a mess to setup, once you give it a nice API frontend that handles most of the more complex CPU/Architecture specific stuff, works somewhat well, you can figure out what type of hardware you have, you know what to do to certain fans, you can read tempetures, and so on. While I hate ACPI, its still a little nice, its usable once you use a dedicated AML interpreter like LAI, uACPI, or ACPICA (which is just a giant mess of things you need to provide ACPICA, but its clean, and at least, somewhat usable)

## Why I love ACPI but also hate it

You see my above opinions are old, ACPI is great now that I think about it more, I do not much like writing, but hey, ACPI is great.

### ACPI is standard(kinda)

Most (decent and modern) ACPI implementations are all the same, standard IOAPIC, AML commands, etc and it all runs smoothly (somewhat) with a proper implementation.

Anyways, have a great day yall! As a great man once said,

```c
#include <fb.h>

void kmain(void) {
    printk("AND THATS ALL FOLKS!\n");
    return;
}
```