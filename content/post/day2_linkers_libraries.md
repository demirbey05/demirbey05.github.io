+++
author = "Okan"
title = "Day 2 - Linking Internals"
date = "2023-10-08"
description = "ELF standard and linking process"
tags = [
    "100dosp",
]
+++

At my previous blog post, I mentioned about linking. Linking is the process of merging a bunch of relocatable object files into single executable. If we think linking as box that have inputs and output, the inputs are **relocatable object file** and output is **executable object file**. These two files must organized according to some format. This format is depending your OS. In Windows, the format is PE(Portable Executable) and ELF(Executable and Linkable Format) in Unix systems. We will use ELF for this blog post.


## Object Files and ELF

The organization of the ELF files are shown below : 

![ELF-Organization](/elf-organization.png)

Let's explain each part of them : 

**ELF Header**: This header gives metadata of the about the system which file is compiled on. This information includes endianness, word size and sizes of sections. Typical elf header is shown below. You can read elf header of any object file by `readelf -h <file>` command.

![ELF-Organization](/elf-header.png)

**Segment Header**: This part is only included in executable object file and it assists loader by containing virtual address space information.(We will return)

**Section Header Table** : In the figure above there are some sections such as `.text`, `.bss` . This header contains descriptions of sections and positions in the file. You can access the section header table by `readelf -S <file>` command.

![ELF-SH](/elf-sh.png)