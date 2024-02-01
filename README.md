# ST ST25DV Discovery kit support for Zephyr RTOS

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

### Build & Run

The application can be built by running:

```shell
west build -b $BOARD ../[APP_FOLDER]
```
where `$BOARD` is the target board.
The custom board is located in the boards subfolder.

```
BOARD="st25dv_mb1283_disco"
```

A sample with lvgl support is provided. You can apply it by running:

```
west build -b $BOARD -p always ./lvgl -p always
```

```shell
west flash
```

For native emulation, go to ~/zephyrproject/zephyr/samples/subsys/display:
```
west build -b native_sim_64 -p always ./lvgl -p always
west build -t run
```

#### Local applications to build
```shell
BOARD="st25dv_mb1283_disco"
west build -b $BOARD -p always ../uart_app -DOVERLAY_CONFIG=prj.conf
```

For now the app uses the first UART, which can be accessed via the same USB port than ST-Link.
```shell
screen /dev/ttyACM0 115200
```

#### Troubleshooting
* Flash using STM32 programmer

```
STM32_Programmer_CLI -c port=SWD freq=4000 --download ./build/zephyr/zephyr.elf
```

You may need to push the black reset button to download correctly, release it before it times out.

* Reset
```
STM32_Programmer_CLI -c port=SWD freq=4000 -rst
```

#### Verifying flashed memory
You can read target memory with:
```
STM32_Programmer_CLI -c port=SWD freq=4000 -r32 0x08000000 0x40
```
Note that -r, -r8 and -r16 sometimes return only zeros, make sure you are using -r32.
