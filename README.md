# A Raspberry Pi Weather Radio

This library adapts the [Raspberry Pi SAME decoder board](http://www.aiwindustries.com/store/p9/Raspberry_Pi_B_%2F2_NWR_Receiver%2FSAME_Decoder.html) to user-level
functionality so that you can focus on your application.  It has
error handling!  It has unit tests!  It has events!  Callbacks!

See the [Presentation slides](https://docs.google.com/presentation/d/1nTsBxVldKxCx8PAM8XSf-2OYdHT5qSjltk65oyRk6Xs/edit?usp=sharing).  

## Build status
[![build status](https://travis-ci.org/ke4roh/RPiNWR.svg?branch=master)](https://travis-ci.org/ke4roh/RPiNWR/branches)
[![Coverage Status](https://coveralls.io/repos/github/ke4roh/RPiNWR/badge.svg?branch=master)](https://coveralls.io/github/ke4roh/RPiNWR?branch=master)

## Features
* Receive, prioritize, and act on SAME alerts
* Extensive error correction for poorly-received messages
* Quick (<.5 sec) response to received messages
* Multi-threaded event model

## Make one!
Here's what you need to do to turn this repository into something that works for you.

### Parts list
You need  a few parts:
* Raspberry Pi 3B
* [AIWIndustries Weather Radio receiver board](http://www.aiwindustries.com/store/p9/Raspberry_Pi_B_%2F2_NWR_Receiver%2FSAME_Decoder.html) + accessories (antenna, case, volume knob)
* 8GB+ micro SD card
* USB power supply

### Installation steps
1. Install Raspbian on the SD card.
2. Put all the parts together.  They only fit one way.
3. Hook it up to a TV and set up WiFi if you wish.  Get it so you can SSH in.
4. Optionally set up [Dataplicity](https://www.dataplicity.com/) so you can log in from anywhere
5. Log in as pi and clone this repo.
6. Set up dependencies:

```bash
sudo apt-get update
sudo apt-get install git python-dev python-smbus geos i2c-tools python-rpi.gpio python3-rpi.gpio libxml2-dev libxslt1-dev python-shapely
# Follow instructions to install i2c kernel support:
#   https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c
git clone https://github.com/nioinnovation/Adafruit_Python_GPIO.git
(cd Adafruit_Python_GPIO; sudo python3 setup.py install)
# now CD to where you cloned this project
sudo ./setup.py test
```

5. Running the radio is simple:
```bash
python3 -m RPiNWR.demo --transmitter WXL58
```

You can specify the transmitter or not, but if you do and the 
transmitter is listed in nwr\_data.py, error correction is 
more robust.  

See demo.py and its tests for information about command line options.

At the moment, this radio implementation lets you subscribe to events
and observe status of the radio over time.  Further development will
add functionality and bring the demo code up to a more practical 
implementation.  

## Where is the internet message stuff and tornado-only alerting?
It's on the dev branch.  It's fresh, really fresh.  So you're encouraged to help with development and testing or just to try it out, but the examples there aren't fully baked yet or else they'd be on the master branch!  As of October 24, 2016, It's pretty close, so stay tuned.

## Helping
Check out the issues in WaffleIO:
[![Stories in Ready](https://badge.waffle.io/ke4roh/RPiNWR.svg?label=ready&title=Ready)](http://waffle.io/ke4roh/RPiNWR)

Please submit your log files as issues! Messages and RSSI reports are 
especially useful at the moment.  

Also, see the next section...

## Developing
Have a look at ```# TODO``` items in the code and the issues to see what
needs to be done.  Pull requests and issues are most welcome!

Adding an Si4707 in a new environment (not RPi, or not the AIWI board)
is straightforward.  Just create a new context that provides the same
functionality as AIWIBoardContext.py for your environment.  Name that
context when you start the radio, and you're up and running.  Please
consider contributing your context via a pull request. 

## License
GNU GPL v. 3 - see the LICENSE file for details

