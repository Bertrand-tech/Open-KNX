# Background
 
There might be cases where your borard gets stuck and you have the impression, it is bricked. Don't worry, this is not the case. the following chapters describe the steps which are necessary to solve this situation.

## Board with SAMD

* connect the board via USB with your computer
* if this board is not powered via USB, connect it also with KNX-Bus
* doubleclick on the reset button, the prog LED should now kind of "pulsing"

## Board with RP2040

* Download the file [flash_nuke.uf2](http://www.elektronik-kompendium.de/sites/raspberry-pi/code/flash_nuke.uf2) on your computer
* press and hold the BOOT-Button on the board
* connect the board via USB with your computer (while holding BOOT)
* You will find now a new USB-Device on your computer called RPI-RP2
* now copy the file flash_nuke.uf2 from your download-location to the new USB-Device

## Final steps for both boards

* Flash the board with a firmware
* program PA from ETS
* program the application from ETS

