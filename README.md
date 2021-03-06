Origin
======

Shamelessly forked from the following repo and very slightly modified for use with the SelfMon VMOD.
https://github.com/kroesche/stellaris_eflash

I have set the ports back to the original for use with the VMOD. The device name will match either
the current beta units, or the newer bootloader when I introduce it.

eflash
======

This is the eflash utility, used for firmware update of Stellaris/Tiva
microcontrollers via ethernet.  This program runs on a host PC and
assumes the "boot_eth" app is running on the MCU and connected to
ethernet network.

License
-------
These files are subject to the original TI license from the StellarisWare
distribution.  I have made some minor modifications, but do not change the
license.  I make no additional restrictions or claims on my modifications.
You are free to use and modifiy further my modified version, but you are
still subject to the original TI license.

Summary
-------

This is the original code from the StellarisWare distribution
(LM3S, revision 10636).  I have modified this to build and run on
a Mac.

I made the following modifications:

* changed type of some variables to C99 types, to ensure correct size
* changed from use of winsock to normal sockets
* added 40000 to all port numbers (explained below)
* add new command line option to specify host IP address
* minor changes to eliminate warnings when compiling on Mac

The original commit to this repo is the unmodified TI version.  If you want
to see the changes I made, you can diff against the first commit.

### Host IP address ###

I had problems with the original code correctly picking up the host
IP address.  For one thing, if you have both wired and wireless connections,
which is used?  Second, it kept picking up the host address as
127.0.0.1.  So I added a new command line switch to specify the host
IP address.  The new command line option is "-l addr" or
"--myip=addr".  See the program usage help for more information.

### Building ###

Because the TI supplied Makefile is oriented around building on a
Windows host, I did not bother to use the Makefile. I just build it
with the following command:

    gcc -o eflash bootp_server.c eflash.c

### Running ###

    sudo ./eflash --myip=10.226.111.66 --ip=10.226.111.53 --mac=d8.b0.4c.55.aa.55 lce-k3-1_2_1_047.bin --verbose

    Where myip is the linux system interface and ip is the module IP.
