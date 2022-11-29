### main.py
```python
from fastapi import FastAPI
from default_temperature import default_temperature
# import serial
# import time

app = FastAPI()


# port_info = 'COM4'
# baudrate_info = 9600
# arduino = serial.Serial(port=port_info, baudrate = baudrate_info)

#@app.get("/")
#    return "hello world"

@app.get("/default_temperature/{default_value}")
def main(default_value: int):
    print("main.py ::" + str(default_value))
    return default_temperature(default_value)
```

### default_temperature.py
```python
import serial

arduino = serial.Serial(port='COM4', baudrate=9600)

def default_temperature(default_value):
    print("asdfasf::"+str(default_value))
    
    # arduino.write('.'+str(default_value))
    arduino.write(str(default_value).encode())

    if arduino.readable():

        response = arduino.readline()
        print("@@@@@@아두이노 => 파이썬@@@@@@")
        print(response[:len(response)-1].decode())
```