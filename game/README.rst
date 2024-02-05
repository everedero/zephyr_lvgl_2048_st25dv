.. zephyr:code-sample:: 2048
   :name: LVGL 2048 game
   :relevant-api: display_interface input_interface

   Launch a 2048 game

Overview
********

This sample application launches a 2048 game.
This is forked from lv_lib_100ask `LV100ask`_

Requirements
************

Board used of this sample is S ST25DV, MB1283 flavour.

Building and Running
********************

Example building for :ref:`st25dv_mb1283_disco`:

.. zephyr-app-commands::
   :zephyr-app: game
   :board: st25dv_mb1283_disco
   :goals: build flash

Example building for :ref:`native_sim <native_sim>`:

.. zephyr-app-commands::
   :zephyr-app: samples/subsys/display/lvgl
   :board: native_sim
   :goals: build run

Alternatively, if building from a 64-bit host machine, the previous target
board argument may also be replaced by ``native_sim_64``.

References
**********

.. target-notes::

.. _LVGL Web Page: https://lvgl.io/
.. _SDL2: https://www.libsdl.org
.. _LV100ask: https://github.com/100askTeam/lv_lib_100ask.git
