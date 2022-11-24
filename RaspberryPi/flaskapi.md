```
from fastapi import FastAPI
from default_temperature import default_temperature
from temperature_management import temperature_management 
from filtering_management import filtering_management
from feeding_management import feeding_management
import serial
import time

app = FastAPI()


port_info = '/dev/ttyACM0'
baudrate_info = 9600
arduino = serial.Serial(port=port_info, baudrate = baudrate_info)

#@app.get("/")
#    return "hello world"

@app.get("/default_temperature/{default_value}")
def main(default_value: int):
    default_value = default_value
    print("main.py ::" + str(default_value))
    return default_temperature(arduino, default_value)

@app.get("/temperature_management")
def main():
    return temperature_management(arduino)


@app.get("/filtering_management")
def main():
    return filtering_management(arduino)

@app.get("/feeding_management")
def main():
    return feeding_management(arduino)

```
