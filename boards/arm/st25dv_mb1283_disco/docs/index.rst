.. _stm25dv_disco_board:

ST ST25DV Discovery, MB1283 version
###################################

Overview
********

The ST25DV04K device is a dynamic NFC/RFID tag IC with a dual interface. It embeds a
4 Kbits EEPROM memory. It can be operated from an I2C interface, or by a 13.56 MHz
RFID reader, or by a NFC phone. The ST25DV04K Class 5 antenna daughter card, included
in the kit, can be replaced by Class 1 or Class 6 antennas.

The ST25DV-DISCOVERY is a demonstration kit to evaluate the features and capabilities
of the ST25DV series.
It is based on the NFC ST25DV04K device embedded on a daughter card using a Class 5 antenna
and a STM32 processor driving a mother board.


.. image:: img/st25dv_mb1283_disco.jpg
     :align: center
     :alt: ST25DV_MB1283_DISCO

Hardware
********

The ST25DV Discovery kit provides the following hardware components:

- Main board: ST25DV_Discovery_Mboard:

  - STM32F405VGT6 LQFP100 32-bit microcontroller, with 1 Mbyte Flash memory, 192 + 4 Kbytes SRAM.
  - LCD color screen (320 x 200 pixels)
  - Touch screen driver
  - Different color LEDs (power, user, ST link)
  - User push button
  - Joystick for menu selection
  - Reset button
  - On board ST link for microcontroller firmware upgrade and debug
  - ST link mini USB
  - User micro USB
  - USB micro or mini connector for board powering
  - Demonstration edition (optional add-on module) with Bluetooth Low Energy module,
    Wi-Fi ® module and JTAG 20 pin connector

It exists in two variants, MB1283 and MB1285.

- Antenna board: ST25DV_Discovery_ANT_C5:

  - 40 mm x 24 mm, 13.56 MHz inductive antenna etched on the PCB
  - ST25DV04K Dynamic NFC / RFID tag
  - I 2 C interface connector
  - Energy harvesting output (VOUT) with a 10nF capacitance filtering circuit
  - GPO configurable as RF WIP/BUSY output, to indicate that an RF operation is ongoing

Default Zephyr Peripheral Mapping:
----------------------------------

- UART_1 TX/RX : PA9/PA10 (ST-Link Virtual Port Com)
- UART_6 TX/RX : PC6/PC7 (Arduino Serial)
- I2C1 SCL/SDA : PB8/PB9 (Arduino I2C)
- I2C4 SCL/SDA : PD12/PB7 (Touchscreen FT6202, PI13 Interrupt Pin)
- SPI2 SCK/MISO/MOSI : PA12/PB14/PB15 (Arduino SPI)
- ETH : PA1, PA2, PA7, PC1, PC4, PC5, PG11, PG13, PG14
- LD1 : PJ13
- LD2 : PJ5
- LD3 : PA12
- LD4 : PD4

Serial Port
===========

The STM25DV Discovery kit has up to 8 UARTs. The Zephyr console output is assigned to UART1
which connected to the onboard ST-LINK/V2 Virtual COM port interface. Default communication
settings are 115200 8N1.

Programming and Debugging
*************************

Applications for the ``stm32f769i_disco`` board configuration can be built and
flashed in the usual way (see :ref:`build_an_application` and
:ref:`application_run` for more details).

Flashing
========

STM25DV Discovery kit includes an ST-LINK/V2 embedded debug tool interface.
This interface is supported by the openocd version included in the Zephyr SDK.

Flashing an application to STM25DV Discovery
-------------------------------------------

First, connect the STM25DV Discovery kit to your host computer using
the USB port to prepare it for flashing. Then build and flash your application.

Here is an example for the :ref:`hello_world` application.

.. zephyr-app-commands::
   :zephyr-app: samples/hello_world
   :board: stm25dv_disco
   :goals: build flash

Run a serial host program to connect with your board:

.. code-block:: console

   $ minicom -D /dev/ttyACM0

You should see the following message on the console:

.. code-block:: console

   TODO

Debugging
=========

You can debug an application in the usual way.  Here is an example for the
:ref:`hello_world` application.

.. zephyr-app-commands::
   :zephyr-app: samples/hello_world
   :board: stm25dv_disco
   :goals: debug


.. _ST25DV-DISCO website:
   https://www.st.com/en/nfc/st25dv-i2c-series-dynamic-nfc-tags.html

.. _ST25DV datasheet:
   https://www.st.com/resource/en/datasheet/st25dv04k.pdf

.. _STM32F40xxx reference manual:
   https://www.st.com/resource/en/reference_manual/rm0090-stm32f405415-stm32f407417-stm32f427437-and-stm32f429439-advanced-armbased-32bit-mcus-stmicroelectronics.pdf
