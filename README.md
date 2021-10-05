# esp32-air-quality-sensor-mqtt

This is a version of my [esp32-air-quality-reader](https://github.com/VirtualWolf/esp32-air-quality-reader) that reads from a [Plantower PMS5003](http://plantower.com/en/content/?108.html) air quality sensor and publishes the results to an MQTT topic. It uses Peter Hinch's [mqtt_as](https://github.com/peterhinch/micropython-mqtt/tree/master/mqtt_as) MicroPython library for MQTT functionality.

It reads the sensor every three minutes, warming it up for 30 seconds beforehand.

## Setup
Create a file called `config.json` at the root of the `src` directory with the following contents:

```json
{
    "client_id": "<MQTT client ID for the ESP32",
    "server": "<address of MQTT broker>",
    "port": 1883,
    "topic": "<MQTT topic to publish to>",
    "ssid": "<wifi network name>",
    "wifi_pw": "<wifi network password>"
}

```

You can optionally add the following to override the default library values of `true` for `clean` and `clean_init`:

```json
    "clean": false,
    "clean_init": false,
```

## Message content
Messages are published as stringified JSON in the following format:

```json
{
    "pm_1_0": 0,
    "pm_2_5": 0,
    "pm_10": 0,
    "particles_0_3um": 0,
    "particles_0_5um": 0,
    "particles_1_0um": 0,
    "particles_2_5um": 0,
    "particles_5_0um": 0,
    "particles_10um": 0
}
```

On an [Adafruit HUZZAH32](https://www.adafruit.com/product/3405), the red LED on the board will light up when it has connectivity to the MQTT broker and will go out when the connectivity stops.
