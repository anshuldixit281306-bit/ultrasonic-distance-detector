# ESP32 ultrasonic-distance-detector

## Overview

This project uses an ESP32 and HC-SR04 ultrasonic sensor to measure distance and activate a buzzer when an object comes within 20 cm.

## Components Required

* ESP32 Development Board
* HC-SR04 Ultrasonic Sensor
* Active Buzzer
* Breadboard
* Jumper Wires


## Working Principle

1. ESP32 sends an ultrasonic pulse.
2. HC-SR04 transmits sound waves.
3. Sound reflects from nearby objects.
4. Echo time is measured.
5. Distance is calculated.
6. If distance is below 20 cm, buzzer turns ON.

## Formula Used

Distance = (Time × 0.034) / 2

Where:

* 0.034 = Speed of sound in cm/µs
* Division by 2 compensates for round-trip travel

## Features

* Real-time distance measurement
* Obstacle detection
* Serial Monitor output
* Simple implementation


# Project Code

```cpp
// Ultrasonic Distance Detector using ESP32

#define TRIG_PIN 5
#define ECHO_PIN 18
#define BUZZER_PIN 19

long duration;
float distance;

void setup() {

  Serial.begin(115200);

  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(BUZZER_PIN, LOW);
}

void loop() {

  // Clear Trigger Pin
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  // Send Ultrasonic Pulse
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Measure Echo Time
  duration = pulseIn(ECHO_PIN, HIGH);

  // Calculate Distance
  distance = duration * 0.034 / 2;

  // Display Distance
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Buzzer Condition
  if(distance < 20){
    digitalWrite(BUZZER_PIN, HIGH);
  }
  else{
    digitalWrite(BUZZER_PIN, LOW);
  }

  delay(500);
}
```

---

# Output Example

Distance: 45 cm
Distance: 28 cm
Distance: 15 cm → Buzzer ON

#image

![project image](https://github.com/anshuldixit281306-bit/ultrasonic-distance-detector/blob/9fbc106172d2e48df5c5b18a4288d24fe08c5993/Screenshot%202026-06-01%20204008.png)

#video

![project video](https://github.com/anshuldixit281306-bit/ultrasonic-distance-detector/blob/4c9f5bba5c5d471bd198b1a44a6de9fcd7b3633e/distance%20detector%20-%20Wokwi%20ESP32%2C%20STM32%2C%20Arduino%20Simulator%20-%20Google%20Chrome%202026-06-01%2020-39-20%20(1).mp4)




