# NOT WEBLOG
__This is just the documentation record for my research on bluetooth for winter pg show. Don't read this file if you are marking me for Final Year Project.__
## 29Nov

[Youtube Tutorial(1 board bluetooth)](https://youtu.be/ZwAcOJukpyI?si=JGOEPyXYUgunOez_)

[code example](https://rootsaid.com/arduino-ble-example/)

[Connecting Nano 33 BLE Devices over Bluetooth](https://docs.arduino.cc/tutorials/nano-33-ble-sense/ble-device-to-device)

[board info](https://store.arduino.cc/products/arduino-nano-33-ble)

```C++
#include <Wire.h>
#include "Adafruit_MPR121.h"
#include <Adafruit_Sensor.h>
#include <Adafruit_BNO055.h>
#include <utility/imumaths.h>

// touch sensor
#ifndef _BV
#define _BV(bit) (1 << (bit)) 
#endif

// orientation
#define BNO055_SAMPLERATE_DELAY_MS (100)
Adafruit_BNO055 bno = Adafruit_BNO055(55, 0x28, &Wire);

// force
#define FORCE_SENSOR_PIN A0 // the FSR and 10K pulldown are connected to A0

Adafruit_MPR121 cap = Adafruit_MPR121();
// touch sensor
uint16_t lasttouched = 0;
uint16_t currtouched = 0;

void setup() {
  Serial.begin(115200);
  
  // touch sensor
  // If tied to SDA its 0x5C and if SCL then 0x5D
  if (!cap.begin(0x5A)) {
    Serial.println("MPR121 not found, check wiring?");
    while (1);
  }
  Serial.println("MPR121 found!");

  // orientation
  if(!bno.begin())
  {
    Serial.print("Ooops, no BNO055 detected ... Check your wiring or I2C ADDR!");
    while(1);
  }
  bno.setExtCrystalUse(true);
}

void loop() {
  // pressure
  int analogReading = analogRead(FORCE_SENSOR_PIN);


  // orientation
    sensors_event_t event;
    bno.getEvent(&event);
    Serial.print("Vector3,");
    Serial.print(event.orientation.x, 4);
    Serial.print(",");
    Serial.print(event.orientation.y, 4);
    Serial.print(",");
    Serial.println(event.orientation.z, 4);
    Serial.print("Pressure:");
    Serial.println(analogReading);
    delay(50);
    
  // touch sesnsor
  currtouched = cap.touched();
  
  for (uint8_t i=0; i<12; i++) {
    // it if *is* touched and *wasnt* touched before, alert!
    if ((currtouched & _BV(i)) && !(lasttouched & _BV(i)) ) {
      //Serial.print(i); 
      Serial.println("Wire:1");//touched
    }
    // if it *was* touched and now *isnt*, alert!
    if (!(currtouched & _BV(i)) && (lasttouched & _BV(i)) ) {
      //Serial.print(i); 
      Serial.println("Wire:0");//released
    }
  }

  // reset our state
  lasttouched = currtouched;

  return; // important!! It works
    
  for (uint8_t i=0; i<12; i++) {
    Serial.print(cap.filteredData(i)); Serial.print("\t");
  }
  
  for (uint8_t i=0; i<12; i++) {
    Serial.print(cap.baselineData(i)); Serial.print("\t");
  }
  
  delay(50);



}
```
