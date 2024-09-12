# Salus-RT505TX-RFM69
This project is designed to control my boiler through Home Assistant and MQTT by replicating the RF messages from my Salus RT505TX thermostat. 

It is an ongoing project and is very much a work-in-progress currently; this is my first foray into RF & CircuitPython.

# Hardware
I am using the [Adafruit Feather RP2040 RFM69](https://learn.adafruit.com/feather-rp2040-rfm69/overview) board for TX/RX of the RF signals; it's an RP2040 microcontroller with a 900MHz RFM69HCW radio module onboard.

To allow the whole thing to connect to my network and MQTT broker, I've included an [AirLift ESP32 WiFi co-processor breakout](https://learn.adafruit.com/adafruit-airlift-breakout). Ultimately the AirLift FeatherWing would have been easier to implement, but they were all out of stock when I started looking.

To wire the two together, I followed [Adafruit's guide](https://learn.adafruit.com/adafruit-airlift-breakout/circuitpython-wifi) which is very clear and easy to follow.

# Libraries
To handle TX/RX of RF, I am utilising the [RFM CircuitPython](https://github.com/adafruit/Adafruit_CircuitPython_RFM/tree/main/adafruit_rfm) library. It's pretty versatile and easy to get up and running quite quickly. However, I had to make a number of small changes to allow for my specific payload to be sent as intended.

To connect to my MQTT broker, I am utilising the MiniMQTT library. It was very simple to set up using [Adafruit's guide](https://learn.adafruit.com/mqtt-in-circuitpython) and the library's [documentation](https://docs.circuitpython.org/projects/minimqtt/en/latest/).

# Salus RT505TX Protocol
Using [Universal Radio Hacker](https://github.com/jopohl/urh) and cheap RTL-SDR receiver, I was able to capture the messages sent by my thermostat & their associated parameters.
- TX frequency: 868.299MHz
- Bitrate: 2.4kbps
- Frequency deviation: 31KHz
