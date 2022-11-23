# This Static Folder contains some Images required for filling form on Play Store.

### >>> Getting error :
![image](https://user-images.githubusercontent.com/50515418/202521001-847bafbe-3289-46fa-a7f0-f70d604308e9.png)

-------------------------------------

- https://github.com/imvickykumar999/Ideationology-Lab/blob/main/Hardwares/Extras/esp32_led/esp32_led.ino#L77
- http://ai2.appinventor.mit.edu/#5050980241375232

- https://console.firebase.google.com/u/1/project/home-automation-336c0/database/home-automation-336c0-default-rtdb/data/~2FA~2FB~2FC~2FSwitch
- https://www.youtube.com/watch?v=yrOMIf8yVxw

- INO Code: https://drive.google.com/file/d/1UzbXXIUXYG0RKR1V6F47Tz8V8RSrIUaX/view
- https://www.youtube.com/watch?v=Z3YdtMsGmjE

--------------------------------------------

    #include <WiFi.h>
    #include "FirebaseESP32.h"
    //#include <Servo.h>
    int servoPin = 2; // D2 PIN
    //Servo Servo1;
    #define WIFI_SSID "Vicky"
    #define WIFI_PASSWORD "*********"
    #define FIREBASE_HOST "home-automation-336c0-default-rtdb.firebaseio.com"
    #define FIREBASE_AUTH "********************************"
    FirebaseData firebaseData;
    void setup() {
    //  Servo1.attach(servoPin);
      Serial.begin(115200);
      WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
      Serial.print("Connecting to Wi-Fi");
      while (WiFi.status() != WL_CONNECTED)
      {
        Serial.print(".");
        delay(300);
      }
      Serial.println();
      Serial.print("Connected with IP: ");
      Serial.println(WiFi.localIP());
      Serial.println();
      Firebase.begin(FIREBASE_HOST, FIREBASE_AUTH);
      Firebase.reconnectWiFi(true);
      //Set database read timeout to 1 minute (max 15 minutes)
      Firebase.setReadTimeout(firebaseData, 1000 * 60);
      pinMode(servoPin, OUTPUT);
    }
    void loop() {
        if (Firebase.getInt(firebaseData,"/A/B/C/Switch"))
        {
          int val2 = (firebaseData.intData());

          if(val2==1){
            digitalWrite(servoPin, HIGH);
            Serial.println("HIGH");
          }

          else{
            digitalWrite(servoPin, LOW);
            Serial.println("LOW");
          }
        }
        delay(200);
      // put your main code here, to run repeatedly:
    }
