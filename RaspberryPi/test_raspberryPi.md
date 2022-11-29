## main.py

```
from fastapi import FastAPI
from serialTest import serialTest

app = FastAPI()

@app.get("/default_temperature/{default_value}")
def main(default_value: int):
    return serialTest(default_value)
```

## serialTest.py

```
import serial

arduino = serial.Serial(port='COM4', baudrate=9600)

def serialTest(default_value):

    arduino.write(str(default_value).encode())

    if arduino.readable():

        response = arduino.readline()
        print("@@@@@@아두이노 => 파이썬@@@@@@")
        print(response[:len(response)-1].decode())
```
