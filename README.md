hex2dfu
=======

Simple command line tool to convert file format from Intel HEX to STM32 DFU.


Compile
=======

hex2dfu is a single C file application and can be easily built by any ANSI C compiler. No makefile required. Just type:

```
gcc -DED25519_SUPPORT=0 hex2dfu.c -o hex2dfu.exe
```

I`m using mingw32 under Windows, change parameters regards your environment.



To enable ED25519 code signing feature, download ED25519 code from https://github.com/encedo/ed25519 
or https://github.com/orlp/ed25519 to folder `ED25519` and type:

```
git clone https://github.com/encedo/ed25519 ED25519
gcc hex2dfu.c ED25519/src/*.c -o hex2dfu.exe
```


Using
=====

1. Simple conversion

   `hex2dfu.exe -i infile.hex -o outfile.dfu`

2. Conversion with changing VID/PID

   `hex2dfu.exe -i infile.hex -o outfile.dfu -p 0x0483 -v 0xdf11`

3. As before with extra device version included (otherwise 0xFFFF will be placed)

   `hex2dfu.exe -i infile.hex -o outfile.dfu -p 0x0483 -v 0xdf11 -d 0x1234`

3. EXTRA: Calculated CRC32 of the file and embed meta data at given address

   `hex2dfu.exe -i infile.hex -o outfile.dfu -c 0x08011000`

4. Code signing: To sign the code ED25519 'secret' need to be provided

   `hex2dfu.exe -i infile.hex -o outfile.dfu -c 0x08011000 -S d4411fa9d5cb6f91b7bd18e4ab41e7d03bf37e1d738c12b923ef0f09de90e6cf`

5. Like above but extra data (-P) are added:

   `hex2dfu.exe -i infile.hex -o outfile.dfu -c 0x08011000 -S d4411fa9d5cb6f91b7bd18e4ab41e7d03bf37e1d738c12b923ef0f09de90e6cf -e -P DEADBEEF`

6. Like above but additional data are public key based on signing secret:

   `hex2dfu.exe -i infile.hex -o outfile.dfu -c 0x08011000 -S d4411fa9d5cb6f91b7bd18e4ab41e7d03bf37e1d738c12b923ef0f09de90e6cf -e`

Automated CRC32 generation is very useful when custom bootloader is in use. We can check firmware at every MCU boot and execute only when file integrity is authenticated. Otherwise perform fail-over (e.g. start USB bootloader). 

Custom USB Bootloader supporting CRC32 checking during boot will be open sourced soon. Stay tuned :)
