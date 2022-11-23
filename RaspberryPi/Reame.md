```
from fastapi import FastAPI
from 
app = FastAPI()

@app.get("/default_temperature")
async def main():
    return default_temperature()

@app.get("/temperature_management")
async def main():
    return temperature_management()

@app.get("/filtering_management")
async def main():
    return filtering_management()

@app.get("/feeding_management")
async def main():
    return feeding_management()
```

```
import serial
import time

def main():

    port = '/dev/ttyUSB0'
    arduino = serial.Serial(port, 9600)

def default_temperature(int default_value):
    
    arduino.write('.'+str(default_value))
    
======================================================

def temperature_management():

    arduino.write('temperature')
    
    temp_value = input()
    
======================================================    

def filtering_management():
    
    arduino.write('filtering')
    turbidity_value = input()

======================================================    

def feeding_management():
    arduino.write('feeding')

======================================================    

if __name__ == "__main__":
    main()
    
        
```
