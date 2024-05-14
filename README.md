# **Arduno_nano_and_Neo6M_GPS_module-based_latitudeand_longitude_tracker**

### Wiring of NEO6M gps-Module to arduino-nao : (Gps lat-long tracker):
![Wiring of Gps lat-long tracker](https://mail.google.com/mail/u/0?ui=2&ik=68b31f5fc2&attid=0.1&permmsgid=msg-a:r-4351644027570747260&th=18f7868b5288bb04&view=fimg&fur=ip&sz=s0-l75-ft&attbid=ANGjdJ9cDMYaR4yY5-oZdYQEdBt3VFEJQHUz8yYRIy-euHQut6M4O3bmT8kscV6L9AA6yu4D1KbYnMUCTeBd3oZ9tzmgXBHKJBBBe77skFRPQFdGlA5ibA8gMNXPXEM&disp=emb&realattid=ii_lw6qnkbk3)


# _ Source Code : _
```Arduino

Source Code : 
#include <Wire.h>
#include <SoftwareSerial.h>
#include <TinyGPS++.h>

#define rxPin 4
#define txPin 3

TinyGPSPlus gps;

SoftwareSerial neogps(rxPin,txPin);

void setup() {

   Serial.begin(9600);
   neogps.begin(9600);

}

void loop() {
  Read_GPS();
}

void Read_GPS(){
  //------------------------------------------------------------------
  boolean newData = false;
  for (unsigned long start = millis(); millis() - start < 1000;)
  {
    while (neogps.available())
    {
      if (gps.encode(neogps.read()))
      {
        newData = true;
        break;
      }
    }
  }
  //------------------------------------------------------------------
  //If newData is true
  if(newData == true){
    newData = false;
    Get_GPS();
  }
  else {
    //no data
  }
}

void Get_GPS(){
   Serial.print( "(" + String(gps.location.lat(),6)+ "," + String(gps.location.lng(),6) + "),");
}

```
