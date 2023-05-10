# Pi--Rfid Reader- Csn150- Final project

# Name of Project

Capturing Card info with Raspberry Pi

## Purpose 

+ To capture card info and to write and read on to new card
+ To capture Key info that allows access to Doors, Cars, etc


## Equipment 
[Raspberry Pi 3 model B+](https://www.amazon.com/ELEMENT-Element14-Raspberry-Pi-Motherboard/dp/B07P4LSDYV/ref=sr_1_3?crid=2A2LYXLB9ADCK&keywords=raspberry+pi+3b&qid=1683315210&sprefix=Raspberry+pi%2Caps%2C98&sr=8-3&ufe=app_do%3Aamzn1.fos.006c50ae-5d4c-4777-9bc0-4513d670b6bc)

[Micro SD card](https://www.amazon.com/Amazon-Basics-microSDXC-Memory-Adapter/dp/B08TJRVWV1/ref=sr_1_1_ffob_sspa?crid=YGEUUGT5R37B&keywords=micro+sd+card&qid=1683315379&sprefix=micro+sd+card+%2Caps%2C102&sr=8-1-spons&psc=1&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUEzUTlYVFMzQTFLR0YmZW5jcnlwdGVkSWQ9QTA5NzA0NzUxUURHVE9OMjdWQ0Q5JmVuY3J5cHRlZEFkSWQ9QTA2Njg3NDYzM1dDMk5KQ0QyMEJZJndpZGdldE5hbWU9c3BfYXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ==)

[Rfid NFC module](https://www.amazon.com/SunFounder-Mifare-Reader-Arduino-Raspberry/dp/B07KGBJ9VG/ref=sr_1_9?crid=3EEXYCDBQY0H2&keywords=raspberry+pi+rfid&qid=1683315512&sprefix=raspberry+pi+rfi%2Caps%2C87&sr=8-9)

[Raspberry Pi OS](https://www.raspberrypi.com/software/)



## Optional 
+ [Raspberry Pi case](https://pimylifeup.com/raspberry-pi-cases/)
+ [Ethernet cable](https://www.amazon.com/s?k=ethernet+cable&i=electronics&linkCode=ll2&linkId=02e41d9fa01024a7d309428447c04a05&tag=pimylifeup-20&ref=as_li_ss_tl)
+ [WiFi](https://www.amazon.com/gp/product/B003MTTJOY/ref=as_li_ss_tl?ie=UTF8&linkCode=ll1&tag=pimylifeup-20&linkId=9328ab6b928f18dc755fc5c52212800b)

## Link for Documentation

https://pimylifeup.com/raspberry-pi-rfid-rc522/



## Recommended 

+ To remote into the Raspberry Pi use VNC 

https://www.realvnc.com/en/connect/download/viewer/


## Steps that we followed 

## Assembling the RFID RC522

One thing you will notice when purchasing an RFID RC522 Reader is that 90% of them don’t come with the header pins already soldered in. The missing pins mean you will have to do it yourself, luckily soldering header pins is a rather simple task, even for beginners.

Wiring your RFID RC522 to your Raspberry Pi is fairly simple, with it requiring you to connect just 7 of the GPIO Pins directly to the RFID reader

![Connectin pi to rfid](https://github.com/NayD101/Pi--Rfid-/blob/main/pi%20rfid%20connect.jpg)


The following steps are from Pimpmylifeup.com 
[How to setup a Raspberry Pi RFID RC522 Chip](https://pimylifeup.com/raspberry-pi-rfid-rc522/)

##Setting up Raspbian for the RFID RC522

 1. Let’s begin by first opening the raspi-config tool, and we can do this by opening the terminal and running the following command.
 + sudo raspi-config

2. This tool will load up a screen showing a variety of different options.
   + On here use the arrow keys to select “5 Interfacing Options“. Once you have this option selected, press Enter.

3.Now on this next screen, you want to use your arrow keys to select “P4 SPI“, again press Enter to select the option once it is highlighted.

4. You will now be asked if you want to enable the SPI Interface, select Yes with your arrow keys and press Enter to proceed. You will need to wait a little bit while the raspi-config tool does its thing in enabling SPI.

5. Once the SPI interface has been successfully enabled by the raspi-config tool you should see the following text appear on the screen, “The SPI interface is enabled“.

Before the SPI Interface is fully enabled we will first have to restart the Raspberry Pi. To do this first get back to the terminal by pressing Enter and then ESC.

Type the following Linux command into the terminal on your Raspberry Pi to restart your Raspberry Pi.
 + sudo reboot

