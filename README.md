# uclibc-sig
IDA multiarch SIG files for uClibc library.

The signatures are generated with IDA Flair 7.1 on **uClibc 0.9.30.1**.

As well explained in [MIRAI source code](https://github.com/jgamblin/Mirai-Source-Code/blob/master/ForumPost.md), uClibc 0.9.30.1 was released with a series of precompiled build environment for different CPU architecture (as x86, MIPS, ARM...). This fact has pushed the Linux IoT malware devs, for the sake of simplicity, to use this particular version of uClibc as static library in their samples.

These signatures permits to recognize library functions inside stripped binaries (in general IoT MIRAI based malwares) making reverse engineering job more easy.

For example:
this is the representation of the content of a x86-64 GafGyt stripped sample before the application of the signatures:
![pre](https://raw.githubusercontent.com/oliveriandrea/uclibc-sig/master/pre.png)

After the application of the signatures:
![post](https://raw.githubusercontent.com/oliveriandrea/uclibc-sig/master/post.png)

I have generated signatures for all Flair supported architectures for the following static libraries:
* ***libc.a***
* ***libcrypt.a***
* ***libdl.a***
* ***libiberty.a***
* ***libm.a***
* ***libnsl.a***
* ***libpthread.a***
* ***libresolv.a***
* ***librt.a***
* ***libutil.a***
* ***uclibc_nonshared.a***

It's possible to use them with IDA and also with radare2.

### Install on IDA
Copy the files in the following locations:

File | Path | Architecture
------------ | ------------- | --------
uclibc_x86.sig | IDADIR/sig/pc | i586, i686
uclibc_x86-64.sig | IDADIR/sig/pc | x86-64
uclibc_arm.sig | IDADIR/sig/arm | armv4l, armv5l
uclibc_ppc.ppc | IDADIR/sig/ppc (**) | ppc, ppc-440fp
uclibc_mips.sig | IDADIR/sig/mips | mips, mipsel
uclibc_sh4.sig | IDADIR/sig/sh3 | sh4

(**) For ppc you have to create the dir.

In order to use them, load your stripped binary then View -> Open subviews ->  Signatures and here right click -> Apply new signature and select uclibc_XXX.
 
 ### Use on radare2
 After loading of the stripped binary enter:
 
 \[0x00400260]> ***zfs PATH_SIGNATURE_FILE***
 
 and it's done!
 
 ### TODO:
 I'm working on related TIL files in order to have also all the MACRO, #define, CONSTANT, ENUM, function definition and arguments extracted from library headers. (Please help me :) )
