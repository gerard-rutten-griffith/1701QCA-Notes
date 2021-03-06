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
Setting up the Micro:bit to write out the analogue value to the serial port and plotting this data on a chart while intermittently playing music nearby produced output as shown below:
![Plot of analogue output](AnaloguePlot.png)

## Test code
Looking at the analogue output, it seems that just measuring the analogue output would be relatively useless to detect sound levels.  What is needed is a way of measuring the _difference_ in analogue values, ie. how much it changes... the amplitude of the changes.  

A crude way to do this is to measure the difference of the analogue reading to the previous analogue reading.  The following code is not the correct way to do this, but it demonstrates the concept.

![Sample Code](AnalogueTest.png)

... and in JavaScript:
``` javascript
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
## Test video
<video src="IMG_1467.mp4" width="512" height="288" controls preload></video>


