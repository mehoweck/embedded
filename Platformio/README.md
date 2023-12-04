# Platform.io


### ATtiny10 support
1. install `AtmelAVR` platform
2. add 'ATtiny10' board definition
There is no `attiny10` chip available by default in `platform.io`. To make it available you first 
have to add it's definition manually. Create the `attiny.json` file in the 
path `%USERPROFFILE%\.platformio\platforms\atmelavr\boards` with the following content: 

```json
{
  "build": {
    "f_cpu": "1000000L",
    "mcu": "attiny10"
  },
  "name": "ATtiny10",
  "upload": {
    "maximum_ram_size": 32,
    "maximum_size": 1024,
    "protocol": "usbasp"
  },
  "url": "http://www.atmel.com/devices/ATTINY10.aspx",
  "vendor": "Atmel"
}
```

3. download newest tollchain
The default toolchain that installed with the platform `AtmelAVR` (now it is 1.70300.191015) have some problem to upload the code into `attiny10`. 
You can resolve the issue by switching to the older tollchain. To do this add the `platform_packages` property in the project connfig file `platformio.json`:

```ini
[env:attiny10]
platform = atmelavr
__platform_packages=toolchain-atmelavr@1.50400.190710__
board = attiny10
upload_flags = -e
build_flags = -v
```

You can also replace the default one with the latest available on  
https://www.microchip.com/en-us/tools-resources/develop/microchip-studio/gcc-compilers/#
The toolchain folder is %USERPROFILE%\.platformio\packages\toolchain-atmelavr_org. 
Rename it, and replace it with the downloaded one. Copy files `.piopm` and `package.json` from the original to the new one.