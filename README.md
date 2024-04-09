# monitoring-soil-moisture-and-nutrient-
monitoring soil moisture and nutrient 
// Include necessary libraries
#include <Servo.h>

// Define pins for sensors
#define MOISTURE_SENSOR_PIN A0
#define NUTRIENT_SENSOR_PIN A1

// Define pins for water and nutrient pumps/valves
#define WATER_PUMP_PIN 2
#define NUTRIENT_PUMP_PIN 3

// Define threshold values
#define MOISTURE_THRESHOLD 400 // Example threshold for soil moisture sensor
#define NUTRIENT_THRESHOLD 300 // Example threshold for nutrient sensor

// Define servo pin for controlling nutrient valve
#define NUTRIENT_VALVE_PIN 9

// Create servo object for nutrient valve
Servo nutrientValve;

void setup() {
  // Initialize serial communication
  Serial.begin(9600);

  // Initialize pins for sensors
  pinMode(MOISTURE_SENSOR_PIN, INPUT);
  pinMode(NUTRIENT_SENSOR_PIN, INPUT);

  // Initialize pins for pumps/valves
  pinMode(WATER_PUMP_PIN, OUTPUT);
  pinMode(NUTRIENT_PUMP_PIN, OUTPUT);

  // Attach servo for nutrient valve control
  nutrientValve.attach(NUTRIENT_VALVE_PIN);
}

void loop() {
  // Read sensor data
  int moistureLevel = analogRead(MOISTURE_SENSOR_PIN);
  int nutrientLevel = analogRead(NUTRIENT_SENSOR_PIN);

  // Check soil moisture level
  if (moistureLevel < MOISTURE_THRESHOLD) {
    // Soil is too dry, activate water pump
    activateWaterPump();
  } else {
    // Soil moisture level is sufficient, deactivate water pump
    deactivateWaterPump();
  }

  // Check nutrient level
  if (nutrientLevel < NUTRIENT_THRESHOLD) {
    // Nutrient level is low, activate nutrient pump/valve
    activateNutrientPump();
  } else {
    // Nutrient level is sufficient, deactivate nutrient pump/valve
    deactivateNutrientPump();
  }

  // Delay before next reading
  delay(1000); // Adjust delay as needed
}

void activateWaterPump() {
  // Example: Activate water pump
  digitalWrite(WATER_PUMP_PIN, HIGH);
}

void deactivateWaterPump() {
  // Example: Deactivate water pump
  digitalWrite(WATER_PUMP_PIN, LOW);
}

void activateNutrientPump() {
  // Example: Activate nutrient pump/valve
  // Example: Control servo to open nutrient valve
  nutrientValve.write(90); // Example angle for opening the valve
  digitalWrite(NUTRIENT_PUMP_PIN, HIGH);
}

void deactivateNutrientPump() {
  // Example: Deactivate nutrient pump/valve
  // Example: Control servo to close nutrient valve
  nutrientValve.write(0); // Example angle for closing the valve
  digitalWrite(NUTRIENT_PUMP_PIN, LOW);
}


