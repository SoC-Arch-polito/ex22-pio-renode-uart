# Simple demo for the usage of platformio and renode

This simple demo shows how to use platformio and renode to develop a simple **zephyr** application.

The targets are the
 - [Freedom-K64F by NXP](https://zephyr-dashboard.renode.io/renodepedia/boards/frdm_k64f/?view=software&demo=Hello_World)
 - [nucleo F410RB](https://zephyr-dashboard.renode.io/renodepedia/boards/nucleo_f410rb)


4 environments are created:
 - One for renode upload with the **K64F**
 - One for renode debug with the **K64F**
 - One for the real hardware upload and debug with the **K64F**
 - One for renode upload with the **nucleo_f410rb**


## K64F and renode

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

