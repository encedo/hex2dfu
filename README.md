hex2dfu
=======

Simple command line tool to convert file format from Intel HEX to STM32 DFU.





Compile
=======

hex2dfu is a single C file application and can be easly compile by any ANSI C compiler. No makefile required. Just type:

gcc hex2dfu.c -o hex2dfu.exe

I`m using mingw32 under Windows, change parameters regards your enviroment.





Using
=====

1. Simple convertion

   hex2dfu.exe -i infile.hex -o outfile.dfu


2. Convertion with changing VID/PID

   hex2dfu.exe -i infile.hex -o outfile.dfu -p 0x0483 -v 0xdf11


3. As before with extra device version included (otherwise 0xFFFF will be placed)

   hex2dfu.exe -i infile.hex -o outfile.dfu -p 0x0483 -v 0xdf11 -d 0x1234


3. EXTRA: Calculated CRC32 of the file and embed meta data at given address

   hex2dfu.exe -i infile.hex -o outfile.dfu -c 0x08011000




Automated CRC32 generation in very usefull when custom bootloader is in use. We can check firmware at every MCU boot and execute only when file ingerrity is authenticated. Otherwise performe failover (e.g. start USB bootloader). 

Custom USB Bootloader supporting CRC32 checking during boot will be open sourced soon. Stay tune :)





