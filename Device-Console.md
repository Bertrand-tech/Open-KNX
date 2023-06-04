Most OpenKNX Devices have a Device Console which can be accessed over USB and a serial console program like putty.

Your serial console should be configured to use LF or CR+LF as new line indication. CR will not work.

## Settings for putty

Download and install [Putty](https://www.putty.org/) if necessary.

You need to find the COM-Port of your OpenKNX-device. The device should be connected to your PC via USB. Open "Device Manager" and look at "Ports":

![Device Manager](https://github.com/OpenKNX/OpenKNX/assets/14316138/e3bc4f20-26d7-47b4-bc7f-41748558a616)

Start putty and enter the following connection settings and press "Open":

![image](https://github.com/OpenKNX/OpenKNX/assets/14316138/6590f240-674a-466d-be43-58fc14f0d0d3)

(REMARK: You need to enter YOUR COM-Port, the one you found in Device Manager!)

In case, you see "weird" line endings, i.e.:

![image](https://github.com/OpenKNX/OpenKNX/assets/14316138/1e226bc1-6e16-4649-b118-b590f85a44f3)

restart the session with an additional setting:

![image](https://github.com/OpenKNX/OpenKNX/assets/14316138/800ae35a-f17d-4e21-89be-94ba87ab11c4)

Afterwards, line endings should be as you are used to:

![image](https://github.com/OpenKNX/OpenKNX/assets/14316138/3319623f-be7a-4f74-8941-dbddd78e71c0)


