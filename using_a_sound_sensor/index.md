# Using a Generic Sound Sensor with the Micro:bit

## What is this Sound Sensor
These are a fairly generic sensor that is marketed towards Arduino, but works just as well with the 3.3 volts power source provided by a Micro:bit.  They are available at [Jaycar](https://www.jaycar.com.au/arduino-compatible-microphone-sound-sensor-module/p/XC4438), [Altronics](https://www.altronics.com.au/p/z6336a-microphone-d-a-module-for-arduino/#/) and of course, eBay.  They are based on an LM393 comparator which has an operating voltage of 2-36v, hence the ability to operate at 3.3v.  
This sensor provides both an analogue and a digital output.  The digital output goes high when a pre-defined sound level is exceeded.  The multi-turn tripot (just a different type of potentiometer) allows adjustment of both the sensitivity and the threshold that triggers the digital output pin.

## Wiring to the Micro:bit
The pins are generally labelled: A0, G, + and D0.

| Label | Description | Micro:bit Pin |
|---|---|---|
| A0 | Analogue output | Any input pin |
| G  | Ground | 0V / GND |
| +  | Input voltage | 3V |
| D0 | Digital output | Any input pin |

## Analysis of the analogue output
I set up the Micro:bit to write out the analogue value to the serial port and then plotted the value on a chart while intermittently playing music nearby.  This is the output:
![Image](missingimage.png)

## Test code
Looking at the analogue output, it seems that just meansuring the analogue output would be relatively useless to detect sound levels.  What is needed is a way of measuring the _difference_ in analogue values, ie. how much it changes - the amplitude of the changes.
A crude way to do this is to measure the difference in the analogue reading to the previous reading.  This is not the correct way to do this, but it demonstrates the concept.  The following image shows the Micro:bit code.
![Image](missingimage.png)
... and in JavaScript:
```
let thisValue = 0
let lastValue = pins.analogReadPin(AnalogPin.P0)
basic.forever(function () {
    thisValue = pins.analogReadPin(AnalogPin.P0)
    led.plotBarGraph(
    Math.abs(thisValue - lastValue),
    50
    )
    lastValue = thisValue
})
```
## Test
<video src="potentiometerv.MP4" width="640" height="480" controls preload></video>


