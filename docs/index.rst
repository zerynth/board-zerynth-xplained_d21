.. _xplained_d21:

Xplained Pro Sam D21
====================

The Xplained Pro Sam D21 is a microcontroller device based on the Atmel `SAMD21J18A ARM Cortex-M0+ CPU <http://www.atmel.com/Images/Atmel-42181-SAM-D21_Datasheet.pdf>`_. The Xplained Pro extension kits offers additional peripherals to extend the features of the device and ease the development of custom designs. It has 22 digital input/output pins, 20 analog inputs, 2 UARTs (hardware serial ports), a 48 MHz clock, 1 TWI, 3 SPI header, a reset button.

One of its most important features is the Atmel Embedded Debugger (EDBG), which provides a full debug interface without the need for additional hardware, significantly increasing the ease-of-use for software debugging. EDBG also supports a virtual COM port that can be used for device and bootloader programming.

.. figure:: /custom/img/XplainedProSamD21.png
   :align: center
   :figwidth: 60% 
   :alt: Xplained Pro Sam D21

   *Xplained Pro Sam D21. Copyright Atmel Corporation*

.. note:: All the reported information are extracted from the official `Xplained Pro Sam D21 page <http://www.atmel.com/tools/ATSAMD21-XPRO.aspx>`_, visit this page for more details and updates.

Pin Mapping
***********

.. figure:: /custom/img/SAMD21_Xplained_PRO_pin_comm.png
   :align: center
   :figwidth: 100%
   :alt: Xplained Pro Sam D21 Pin Mapping

Xplained Pro Sam D21 Official Schematic, Reference Design and Pin Mapping are available on the official `Atmel User Guide <http://www.atmel.com/Images/Atmel-42220-SAMD21-Xplained-Pro_User-Guide.pdf>`_.


Flash Layout
************

The internal flash of the Xplained Pro Sam D21 is organized as a single bank of 256k. Zerynth VM starts at first address of the flash memory.

Device Summary
**************

* Microcontroller: ATSAMD21J18
* Operating Voltage: 3.3V
* Digital I/O Pins (DIO): 22
* Analog Input Pins (ADC): 20
* UARTs: 2
* SPIs: 3
* I2Cs: 1
* Flash Memory: 256 KB
* SRAM: 32 KB
* Clock Speed: 48 MHz

Power
*****

The Xplained Pro Sam D21 can be powered via the USB connector or with an external power supply via "GND" and "5.0 IN" pins of the PWR header.

The device can operate on an external supply of 5V ±2% (±100mV) for USB host operation or from 4.3V to 5.5V if USB host operation is not required. Current recommended requirements, in external power supply mode, are:

* minimum 1A to be able to provide enough current for connected USB devices and the	device itself.
* maximum is 2A due to the input protection maximum current specification

.. note:: External power is required when 500mA from a USB connector is not enough to power the device with possible extension boards. A connected USB device in a USB host application might easily exceed this limit.

Connect, Register, Virtualize and Program
*****************************************

The Xplained Pro Sam D21 debug port is connected to EDBG, which provides a virtual COM port to software on a connected computer. To recognize the device, all **Windows** (automatic driver software installation), **OSX** and **Linux** machines will recognize the device as a COM port automatically.

.. note:: **For Linux Platform**: to allow the access to serial ports the user needs read/write access to the serial device file. Adding the user to the group, that owns this file, gives the required read/write access:
				
				* **Ubuntu** distribution --> dialout group
				* **Arch Linux** distribution --> uucp group

			If the device is still not recognized or not working, the following udev rules may need to be added: ::

			    # Check SUBSYSTEM
			    SUBSYSTEMS=="hidraw", KERNEL=="hidraw*", MODE="0666", GROUP="dialout"

			    # Xplained Pro SamD21 Device
			    SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2111", MODE="0666", GROUP="users", ENV{ID_MM_DEVICE_IGNORE}="1"
			    SUBSYSTEMS=="tty", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2111", MODE="0666", GROUP="users", ENV{ID_MM_DEVICE_IGNORE}="1"




EDBG is also connected to the SAMD21 hardware UART. Serial on pins RX0 and TX0 provides Serial-to-USB communication for programming the device through Atmel EDBG.

Once connected on a USB port the Xplained Pro Sam D21 device is recognized by Zerynth Studio. The next steps are:

* **Select** the Xplained Pro Sam D21 on the **Device Management Toolbar**;
* **Register** the device by clicking the "Z" button from the Zerynth Studio;
* **Create** a Virtual Machine for the device by clicking the "Z" button for the second time;
* **Virtualize** the device by clicking the "Z" button for the third time.

.. note:: No user intervention on the device is required for registration and virtualization process

After virtualization, the Xplained Pro Sam D21 is ready to be programmed and the Zerynth scripts **uploaded**. Just **Select** the virtualized device from the "Device Management Toolbar" and **click** the dedicated "upload" button of Zerynth Studio and **reset** the device by pressing the Reset on-board button when asked.

Power Management and Secure Firmware
************************************

Power Management feature allows to optimize power consumption by putting the device in low consumption state.

Secure Firmware feature allows to detect and recover from malfunctions and, when supported, to protect the running firmware (e.g. disabling the external access to flash or assigning protected RAM memory to critical parts of the system).

Both these features are strongly platform dependent; more information at :ref:`Power Management - Microchip SAMD21 section <pwr-samd21>` and :ref:`Secure Firmware - Microchip SAMD21 section <sfw-samd21>`.
