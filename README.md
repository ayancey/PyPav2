# PyPav2

**This is a work in progress** 

A very simple python module for the Pavlok 2 habit breaker device.
The module is essentially just a wrapper for the linux tool gatttool that will allow for all Pavlok app functionality and then some.

# Requirements:
- tested on python 2.7.13 and 3.5.3
- pexpect module 
- gatttool (bluetooth low energy tool, standard in ubuntu with Bluez, requires BLE capable device)

# Stimulus Arguments:
- level: a percentage from 0% - 100%
- count: number of times to repeat stimulus 0 - 7
- duration_on: stimulus duration in seconds (max 10 seconds, minimum .11 seconds) **beep and vibrate only**
- gap: time in milliseconds between simulus repetitions (see restrictions above ^) **beep and vibrate only**
- example: device.beep(100, 2, 1, 1)

- **duration equation:**
For a reason I have yet to uncover, the Pavlok 2 uses a duration of max 63 (0x3e) which is about 10 seconds. I sampled every level 0-63 with as much accuracy as I could and came up with an exponential regression. The formula is y = 0.104*e^(0.0745x), y being seconds and x being duration value (0-63).

# Usage
    from pav import Pavlok
    device = Pavlok(mac="mac:address:of:your:device")
    device.beep(100)
    device.shock(5)

This is a hobby project by every definition of the word, and I am working to implement every feature that the official Pavlok mobile app allows and a few extras.
Originally created for use in behavioral psychology experiments, this repo is now just a project I maintain for fun. Hope it helps anyone else who is interested! 

Video example of code functioning (using raspberry pi zero w)
https://youtu.be/dpEqDgbgF_0
