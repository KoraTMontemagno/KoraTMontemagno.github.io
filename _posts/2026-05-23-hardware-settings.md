---
title: 1. Hardware settings
excerpt: How do you connect a sex toy to a computer bypassing the commercial apps? 
categories:
- Tutorials
---

If we want to test evoked potentials with EEG in response to a pleasurable sexual stimulus, we need to have a reliable way to deliver the stimulus, get a response, and get the exact activation time of the device you are using to understand how to epoch the EEG signal (this is referred to as EEG trigger).

<!-- more -->

I could think about two different ways to approach this problem.

The first one is to have a cable solution (I have seen it done with Arduino) in which a computer is connected to some tool capable of generating vibration/stroke etc, that is connected to the EEG machine, providing a trigger. As very inexperienced with Arduino, I naturally tend to dislike this solution - as it is not the most entry level one; in addition, the vibrator risks not to be compatible with genital stimulation, that could make it a bit harder for us researcher to get approval with that uses (but I know at least a group that managed to do that with this setting).


I needed something more ready to play with and dumb friendly.


So we come to the second solution - using a commercial sex toy and connecting via bluetooth. The main downside of this is that we have to find another way to get the correct timings for the triggers (we will explore it in another post - but we could use an EEG electrode or an accelerometer). Today we will focus on the hardware and software configuration that will allow us to connect a sextoy to your computer.


For this recipe you will need:
- A computer (no idea of specs, sorry) :D
- Python (I used version 3.12) with [buttplug](https://github.com/buttplugio/buttplug-py) package installed
- [Intiface Central](https://intiface.com/): this will allow us to connect with the device
- [Buttplug.io](https://buttplug.io/)
- A sex toy capable of bluetooth connection - I used [Satysfier's dual love](https://www.satisfyer.com/dk/en/satisfyer-dual-love-connect-app?srsltid=AfmBOoqy-77lkGS242cNswD6RFosGqNBY0BH6J_K7G8_dVqLCzPtrkGm), as it has both a vibrator and a clitsucker
- A bluetooth 4.0 USB dongle (I used [this one](https://superprice.dk/shop/computer/pc-tilbehoer/kabler/adaptere-konvertere/bluetooth-csr-4-0-usb-dongle/?gad_source=1&gad_campaignid=17339244643&gbraid=0AAAAADw5jTYmKLM_x1ZfuWF77bLCihbFO&gclid=Cj0KCQjwoMXQBhDcARIsAH-eEtvO9CTTrcehavjiIkQxp6Dj_9NCeuTBZzb1UwEmiym5ZNYMLQ_yH_8aAttBEALw_wcB), but you can easily find some that will ship in your country :))

Once installed all the packages, you should be able to connect the bluetooth device to your computer + USB dongle (follow the instructions [here](https://intiface.com/docs/intiface-central/brands/satisfyer)), and to start the intiface communication.

Now we just need to code! We will use asyncio and buttplug for this part.
The following code is taken from the buttplug README for Python [here](https://github.com/buttplugio/buttplug-py), I have just commented something to make it easier to understand

```
# Import dependencies
import asyncio
from buttplug import ButtplugClient, DeviceOutputCommand, OutputType

# We have to first define the function, and only afterwards call it with asyncio

async def main():
    # Create a client 
    client = ButtplugClient("My App")

    # Connect to Intiface Central (default address)
    await client.connect("ws://127.0.0.1:12345")

    # Scan for devices
    await client.start_scanning()
    await asyncio.sleep(5)  # Wait for devices to be found
    await client.stop_scanning()

    # Control devices
    for device in client.devices.values():
        print(f"Found: {device.name}") # This will be the name of your device

        if device.has_output(OutputType.VIBRATE): #devices can have different way of moving, we are looking for vibrate that applies both to the wibrator and the clitsucking
            await device.run_output(DeviceOutputCommand(OutputType.VIBRATE, 0.5)) # this is the vibration, 0.5 is the intensity 8from 0 to 1, or from 0 to 100 base on your device)
            await asyncio.sleep(2)
            await device.stop()

    await client.disconnect()

asyncio.run(main())
```

This is just the simplest example - in the course of the next posts we will see how to incorporate this feature in a loop, and possibly how to create a simple experiment in Psychopy.