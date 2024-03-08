# ST ST25DV Discovery kit support for Zephyr RTOS

Runs a nice 2048 game on a discontinued ST eval kit, using Zephyr RTOS and LVGL module.

The game app is partially forked from [lv\_lib\_100ask](https://github.com/100askTeam/lv_lib_100ask.git)

Current app is compatible with Zephyr 3.6.0-rc2 (with hwv1).

## Getting Started

Before getting started, make sure you have a proper Zephyr development
environment. You can follow the official
[Zephyr Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html).

### Initialization

If you installed Zephyr scripts in a virtenv:

```shell
source ~/zephyrproject/.venv/bin/activate
```

Then call Zephyr environment init script
```
source ~/zephyrproject/zephyr/zephyr-env.sh
```

#### Local applications to build
```shell
BOARD="st25dv_mb1283_disco"
west build -b $BOARD -p always ./game -DOVERLAY_CONFIG=prj.conf
```

"west flash" does not work, flash using STM32\_Programmer\_CLI - it is somewhere
in your system when you install STM32CubeProgrammer.

```shell
STM32_Programmer_CLI -c port=SWD freq=4000 --download ./build/zephyr/zephyr.elf
```

For now the app uses the first UART, which can be accessed via the same USB port than ST-Link.
```shell
screen /dev/ttyACM0 115200
```

In order to run the native simulation, change the overlay in CMakelists.conf:

```
set(DTC_OVERLAY_FILE "${CMAKE_CURRENT_SOURCE_DIR}/../boards/native_sim_64.overlay")
```

And run:
```
west build -b native_sim_64 -p always ./game -DOVERLAY_CONFIG=prj.conf
./build/zephyr/zephyr.exe
```

Keyboard arrow keys and enter are mapped to 5-way buttons directions.

#### Troubleshooting
* Flash using STM32 programmer fails

```
STM32_Programmer_CLI -c port=SWD freq=4000 --download ./build/zephyr/zephyr.elf
```

You may need to push the black reset button to download correctly, release it before it times out.

* Reset
```
STM32_Programmer_CLI -c port=SWD freq=4000 -rst
```

* Display issues

A synchronisation issue can prevent all the display SPI messages to be sent to the peripheral (missing 0x2a and 0x2b messages),
resulting in a horizontal line being updated instead of squares on all the screen.

Issue https://github.com/zephyrproject-rtos/zephyr/issues/68815 is fixed in Zephyr version > 3.6.0.

#### Verifying flashed memory
You can read target memory with:
```
STM32_Programmer_CLI -c port=SWD freq=4000 -r32 0x08000000 0x40
```
Note that -r, -r8 and -r16 sometimes return only zeros, make sure you are using -r32.
