_This README and all other documentation and software in this repository are covered by the attached MIT license. Nothing in this repository should be construed as a recommendation or assertion that something is safe, legal or otherwise a good idea. Connecting a heater or any other electric device to a computer could do terrible things, like burn your house down. I’m not responsible for anything that happens if you choose to use this knowledge, so MAKE USE OF IT EXCLUSIVELY AT YOUR OWN RISK._

# An automated sauna -- why?

Sauna's take a while to heat up. In my case, about 45 minutes for 85º Celsius. So, it is handy to be able to start it remotely -- for example at the gym -- so that the sauna is ready when I get home.

Unfortunately, most sauna's are not wired for this. They are pretty dumb, and while there are remote start modules for some sauna's, they are expensive and often require specific conrol units and heaters. If you didn't take this into account when you bought it, and paid quite a bit extra for it, you have no official options.

My sauna heater has no built-in thermostat. It has an on/off knob with a timer that turns the sauna on for 4 hours maximum, and then it switches off again.

The purpose of this project was to allow me to turn my sauna on remotely, or schedule it to be turned on. I also wanted thermostat functionality, allowing me to set my heater to a specific temperature rather than gradually getting hotter over time or having to manually turn it off and on all the time. Since I was busy anyway, I also added smart lights to my sauna that can change color and are easily dimmable. Finally, I wanted to be able to control all of this this via my phone but also with hardware buttons on the sauna itself. When you're chilled out after a sauna session, the last thing you want to do is have to find your phone to turn the sauna off -- you want a physical button for that.

I am writing this up so other might make less mistakes than I did trying to get all of this to work. It is not meant as a finished solution: tweak it and make it your own.

# Sauna requirements



# System components

It was my goal to create a system components that are as independent as possible, and to always be able to fall back to manual control of the sauna heater in case any of the smart components fail. The automation setup consists of the following components:

1. **A heavy-duty switch to turn the sauna on and off.** After two failed experiments with some lighter switches, this [Aeotec Heavy Duty Switch](https://aeotec.com/outdoor-z-wave-switch/) was a great find. It is rated for up to 40 amp which should be plenty for most home saunas. It uses the Z-Wave protocol.

2. **A temperature sensor.** Essential for thermostat functionality. I opted for a [Shelly 1PM](https://shelly.cloud/shelly-1pm-wifi-smart-relay-home-automation/) with the [temperature addon](https://shop.shelly.cloud/temperature-sensor-addon-for-shelly-1-1pm-wifi-smart-home-automation#312). This uses a DS18B20 sensor which is rated -55º to +125º, which should be plenty for even the most intense sauna sessions.

3. **Smart lights**. Since I have Philips Hue lights throughout my home it was simplest to get [these](https://www2.meethue.com/en-us/p/hue-white-and-color-ambiance-1-pack-gu10/046677542337). They are not officially rated for the kinds of temperatures a sauna sees, but there is cover between the lights and the sauna which takes some of the heat off them, and so far they have been working well (🤞).

4. **Control software** to create the software thermostat, listen for hardware button presses, integrate with HomeKit, monitor energy usage and some other automation niceties. I use a Raspberry Pi with an [Aeotec Z-wave Stick](https://aeotec.com/z-wave-usb-stick/) and running Home Assistant.

# Switch, Temperature Sensor and Smart Lights

Setting up the Aeotec Heavy Duty Switch is pretty straight forward, though make sure you get heat-proof electricity cable of the appropriate thickness (2.5mm wires in my case) for the capacity of your sauna heater.

One annoying aspect of the Aeotec switch is that its hardware on/off button is hidden behind a cover. Since I will not be using the switch outdoor anyway, I drilled a hole in this cover to expose the button. This allows me to always be able to turn the sauna on and off, even if all of the automation stuff breaks.

For the temperature sensor, I got a simple [waterproof junction box](https://www.google.com/search?q=junction+box+ip65&tbm=isch). Inside I split the incoming AC electricity to the Aeotec Heavy Duty Switch (connected to the sauna heater) and the Shelly 1PM with Temperature addon. I then added the power to the Hue lights to the Shelly switch. That last bit did not gain me much in automation options, but it did reduce the amount of wires in the junction box.

So I have AC coming into the junction box. Then a big fat AC wire coming out running to the Aeotech Heavy Duty Switch for the sauna, and two thinner (but also heat-proof) cables going out for the sauna lights and temperature sensor. These go into the sauna wall and out through the top, running over the roof.

For the temperature sensor itself, I drilled a hole in the sauna wall where I wanted to place it, and another hole at the top of the sauna to run the wire through. I then embedded the sensor into a little block of wood and screwed that into the sauna wall.

# Control Software




Switch
After experimenting with some lighter switches that all broke or gave overload warnings due to my sauna actually using a bit more energy than it is rated for, 




# Prior art
This project was heavily inspired by [William Henderson's SaunaKit](https://github.com/quicklywilliam/saunakit)