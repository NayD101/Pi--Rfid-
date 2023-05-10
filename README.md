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
  sudo raspi-config

2. This tool will load up a screen showing a variety of different options.
   + On here use the arrow keys to select “5 Interfacing Options“. Once you have this option selected, press Enter.

3.Now on this next screen, you want to use your arrow keys to select “P4 SPI“, again press Enter to select the option once it is highlighted.

4. You will now be asked if you want to enable the SPI Interface, select Yes with your arrow keys and press Enter to proceed. You will need to wait a little bit while the raspi-config tool does its thing in enabling SPI.

5. Once the SPI interface has been successfully enabled by the raspi-config tool you should see the following text appear on the screen, “The SPI interface is enabled“.

Before the SPI Interface is fully enabled we will first have to restart the Raspberry Pi. To do this first get back to the terminal by pressing Enter and then ESC.

Type the following Linux command into the terminal on your Raspberry Pi to restart your Raspberry Pi.
  sudo reboot

6.Once your Raspberry Pi has finished rebooting, we can now check to make sure that it has in fact been enabled. The easiest way to do this is to run the following command to see if spi_bcm2835 is listed.
lsmod | grep spi

## Getting Python ready for the RFID RC522

1. Before we start programming, we first need to update our Raspberry Pi to ensure it’s running the latest version of all the software. Run the following two commands on your Raspberry Pi to update it.

sudo apt update
sudo apt upgrade


2.Now the final thing we need before we can proceed is to install python3-dev, python-pip and  git packages. Simply run the following command on your Raspberry Pi to install all of the required packages for this guide on setting up your RFID reader.

sudo apt install python3-dev python3-pip

3.To begin, we must first install the Python Library spidev to our Raspberry Pi using the python “pip” tool that we downloaded in the previous step.

The spidev library helps handle interactions with the SPI and is a key component to this tutorial as we need it for the Raspberry Pi to interact with the RFID RC522.

Run the following command  on your Raspberry Pi to install spidev to your Raspberry Pi through pip.

Please note that we use sudo here to ensure that the package is installed so that all users can utilize it and not just the current user.

sudo pip3 install spidev


4.Now that we have installed the spidev library to our Raspberry Pi we can now now proceed to installing the MFRC522 library using pip as well.
To install the MFRC522 library to your Raspberry Pi using pip go ahead and run the following command.

sudo pip3 install mfrc522

## Writing with the RFID RC522

1. Now lets start off by making a folder where we will be storing our couple of scripts.

We will be calling this folder “pi-rfid”, create it by running the following command.

mkdir ~/pi-rfid

2. Begin by changing directory into our newly cloned folder, and begin writing our Write.py Python script.

cd ~/pi-rfid

sudo nano Write.py

3.Within this file, write the following lines of code. This code will basically ask you for text to input and then write that text to the RFID Tag.


#!/usr/bin/env python


import RPi.GPIO as GPIO


from mfrc522 import SimpleMFRC522


reader = SimpleMFRC522()


try:
        
        text = input('New data:')
        
        print("Now place your tag to write")
        
        reader.write(text)
        
        print("Written")

finally:
        
        GPIO.cleanup()
 
4.Once you have finished writing in your script, it should look something like shown above.

Once you are happy that the code looks correct, you can save the file by pressing CTRL + X then pressing Y and then finally hitting ENTER.

5. Now that we have written our script, we will want to test it out. Before testing out the script make sure that you have an RFID tag handy. Once ready, type the following command into your Raspberry Pi’s terminal.

sudo python3 Write.py

6. You will be asked to write in the new data, in our case we are going to just type in CSN150 as its short and simple. Press Enter when you are happy with what you have written.

7.With that done, simply place your RFID Tag on top of your RFID RC522 circuit. As soon as it detects it, it will immediately write the new data to the tag. You should see “Written” appear in your command line if it was successful.

You can look at our example output below to see what a successful run looks like.


pi@raspberrypi:~/pi-rfid $ sudo python3 Write.py
New data:CSN150
Now place your tag to write
Written

8. You have now successfully written your Write.py script, and we can now proceed to show you how to read data from the RFID RC522 in the next segment of this tutorial.

## Reading with the RFID RC522

Now that we have written our script to write to RFID tags using our RC522 we can now write a script that will read this data back off the tag.

1.Let’s start off by changing the directory to make sure we are in the right place, and then we can run nano to begin writing our Read.py script.

cd ~/pi-rfid

sudo nano Read.py

2. Within this file, write the following lines of code. This script will basically sit and wait till you put your RFID tag on the RFID RC522 reader, it will then output the data it reads off the tag.

#!/usr/bin/env python

import RPi.GPIO as GPIO

from mfrc522 import SimpleMFRC522

reader = SimpleMFRC522()

try:
        id, text = reader.read()
        print(id)
        print(text)
        
 finally:
        GPIO.cleanup()
        
3. Now that you have finished writing your Read.py script for your RFID RC522 it should look something like what is shown below.

#!/usr/bin/env python

import RPi.GPIO as GPIO
from mfrc522 import SimpleMFRC522

reader = SimpleMFRC522()

try:
        id, text = reader.read()
        print(id)
        print(text)
finally:
        GPIO.cleanup()
        

Once you are sure you have entered the code correctly, you can save the file by pressing Ctrl + X then pressing Y and then finally hitting ENTER.

4. Now that we have finally finished our Read.py script we need to test it out. Before we test out the script, grab one of the RFID tags that you want to read. Once that you are ready, type the following command into your Raspberry Pi’s terminal.

sudo python3 Read.py

5. With the script now running, all you need to do is place your RFID Tag on top of your RFID RC522 circuit. As soon as the Python script detects the RFID tag being placed on top, it will immediately read the data and print it back out to you.

6.If you successfully receive data back from your Read.py script with the text that you pushed to the card using your Write.py script then you have successfully set up your Raspberry Pi to connect with your RFID RC522 Circuit.



