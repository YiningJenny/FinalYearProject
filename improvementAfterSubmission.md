# NOT WEBLOG
__This is just the documentation record for my research on bluetooth for winter pg show. Don't read this file if you are marking me for Final Year Project.__
## 29Nov

[Youtube Tutorial(1 board bluetooth)](https://youtu.be/ZwAcOJukpyI?si=JGOEPyXYUgunOez_)

[code example](https://rootsaid.com/arduino-ble-example/)

[Connecting Nano 33 BLE Devices over Bluetooth](https://docs.arduino.cc/tutorials/nano-33-ble-sense/ble-device-to-device)

[board info](https://store.arduino.cc/products/arduino-nano-33-ble)

### F_M_B Original code

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
### F_M_B integrated with Nano 33(currently work) code
```C++
/*
  BLE_Peripheral.ino

  This program uses the ArduinoBLE library to set-up an Arduino Nano 33 BLE 
  as a peripheral device and specifies a service and a characteristic. Depending 
  of the value of the specified characteristic, an on-board LED gets on. 

  The circuit:
  - Arduino Nano 33 BLE. 

  This example code is in the public domain.
*/

#include <ArduinoBLE.h>
      
enum {
  GESTURE_NONE  = -1,
  GESTURE_UP    = 0,
  GESTURE_DOWN  = 1,
  GESTURE_LEFT  = 2,
  GESTURE_RIGHT = 3
};

const char* deviceServiceUuid = "19b10000-e8f2-537e-4f6c-d104768a1214";
const char* deviceServiceCharacteristicUuid = "19b10001-e8f2-537e-4f6c-d104768a1214";

int gesture = -1;

BLEService gestureService(deviceServiceUuid); 
BLEByteCharacteristic gestureCharacteristic(deviceServiceCharacteristicUuid, BLERead | BLEWrite);
/*========================================================== F_M_B=========================================================================*/
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

/*========================================================== F_M_B=========================================================================*/


void setup() {
  Serial.begin(115200);
  while (!Serial);  
  
  pinMode(LEDR, OUTPUT);
  pinMode(LEDG, OUTPUT);
  pinMode(LEDB, OUTPUT);
  pinMode(LED_BUILTIN, OUTPUT);
  
  digitalWrite(LEDR, HIGH);
  digitalWrite(LEDG, HIGH);
  digitalWrite(LEDB, HIGH);
  digitalWrite(LED_BUILTIN, LOW);

  
  if (!BLE.begin()) {
    Serial.println("- Starting Bluetooth® Low Energy module failed!");
    while (1);
  }

  BLE.setLocalName("Arduino Nano 33 BLE (Peripheral)");
  BLE.setAdvertisedService(gestureService);
  gestureService.addCharacteristic(gestureCharacteristic);
  BLE.addService(gestureService);
  gestureCharacteristic.writeValue(-1);
  BLE.advertise();

  Serial.println("Nano 33 BLE (Peripheral Device)");
  Serial.println(" ");

  //===============================================F_M_B=================================================
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
  //==================================================================================================
}

void loop() {
  BLEDevice central = BLE.central();
  Serial.println("- Discovering central device...");
  delay(50);

  if (central) {
    Serial.println("* Connected to central device!");
    Serial.print("* Device MAC address: ");
    Serial.println(central.address());
    Serial.println(" ");

    while (central.connected()) {
      if (gestureCharacteristic.written()) {
         gesture = gestureCharacteristic.value();
         writeGesture(gesture);
       }
    }
    
    Serial.println("* Disconnected to central device!");
  }
  //=================================================================================F_M_B================================================================
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
  //===============================================F_M_B=====================================================
}

void writeGesture(int gesture) {
  Serial.println("- Characteristic <gesture_type> has changed!");
  
   switch (gesture) {
      case GESTURE_UP:
        Serial.println("* Actual value: UP (red LED on)");
        Serial.println(" ");
        digitalWrite(LEDR, LOW);
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDB, HIGH);
        digitalWrite(LED_BUILTIN, LOW);
        break;
      case GESTURE_DOWN:
        Serial.println("* Actual value: DOWN (green LED on)");
        Serial.println(" ");
        digitalWrite(LEDR, HIGH);
        digitalWrite(LEDG, LOW);
        digitalWrite(LEDB, HIGH);
        digitalWrite(LED_BUILTIN, LOW);
        break;
      case GESTURE_LEFT:
        Serial.println("* Actual value: LEFT (blue LED on)");
        Serial.println(" ");
        digitalWrite(LEDR, HIGH);
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDB, LOW);
        digitalWrite(LED_BUILTIN, LOW);
        break;
      case GESTURE_RIGHT:
        Serial.println("* Actual value: RIGHT (built-in LED on)");
        Serial.println(" ");
        digitalWrite(LEDR, HIGH);
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDB, HIGH);
        digitalWrite(LED_BUILTIN, HIGH);
        break;
      default:
        digitalWrite(LEDR, HIGH);
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDB, HIGH);
        digitalWrite(LED_BUILTIN, LOW);
        break;
    }      
}
```

