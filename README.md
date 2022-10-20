# Simple demo for the usage of platformio and renode

This simple demo shows how to use platformio and renode to develop a simple **zephyr** application.

The target is the [Freedom-K64F by NXP](https://www.nxp.com/design/development-boards/freedom-development-boards/mcu-boards/freedom-development-platform-for-kinetis-k64-k63-and-k24-mcus:FRDM-K64F)

Two environments are created
 - One for renode
 - One for the real hardware

For the renode env, you need to create a simple **k64f.resc** script, as renode does not provide a script for this platform.

```
:name: K64F
:description: This script creates a machine and loads the K64F platform

:just to type less
using sysbus

:create machine and load platform
mach create "K64F"
machine LoadPlatformDescription @platforms/cpus/nxp-k6xf.repl
```
The file needs to be placed in the single-node scripts folder of your renode installation. On linux that is:

```bash
/opt/renode/scripts/single-node/
```

The application simply reads lines from an UART, and echo the lines back to the user with some additional info.

The example is inspired by this [zephyr post](https://www.zephyrproject.org/developing-zephyr-rtos-embedded-applications-on-platformio-and-simulating-on-antmicro-renode/).

For testing purposes, the app opens an analyzer for the uart, and creates a socket in the port **3456**. From the host it is possible to access the uart by connecting to the port with:

```bash
$ telnet localhost 3456
```

