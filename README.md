# raspi_humidity
temp and humidity sensor via raspi
DHT 22 Sensor
https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf?scrlybrkr=8f7cc0a0

This guide is pretty good! https://pimylifeup.com/raspberry-pi-humidity-sensor-dht22/
Also, install this: 

sudo apt-get install gpiod
sudo apt-get install libgpiod-dev

------------------------------
This is the code for the libraries and communicating w sensor. Save as humidity.py
import time
import adafruit_dht
import board

dht_device = adafruit_dht.DHT22(board.D4)

while True:
    try:
        temperature_c = dht_device.temperature
        temperature_f = temperature_c * (9 / 5) + 32

        humidity = dht_device.humidity

        print("Temp:{:.1f} C / {:.1f} F    Humidity: {}%".format(temperature_c, temperature_f, humidity))
    except RuntimeError as err:
        print(err.args[0])

    time.sleep(2.0)
    ------------------------------

Setup SSH, VNC

A key point from the guide is #6 :
Once the virtual environment has been generated, we will need to tell the terminal to utilize it as its source.

You will need to run this command every time you want to interact with your DHT22 humidity sensor script. The reason for this is the Python library we are using will be installed only to this environment--

(So after you make yr py script...)

ssh weatherman@sas-weather-he-mdf

source env/bin/activate

then type

python3 humidity.py

If instance is already running, you may have to kill libgpiod first.

I am working on scripts to handle a bunch of this.
Also learning how to display data to a webpage.

