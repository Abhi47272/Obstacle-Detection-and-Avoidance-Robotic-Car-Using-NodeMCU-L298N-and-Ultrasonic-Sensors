#include <NewPing.h>
#define TRIG_PIN 5
#define ECHO_PIN 4
#define LEFT_MOTOR_PIN1 14
#define LEFT_MOTOR_PIN2 12
#define RIGHT_MOTOR_PIN1 13
#define RIGHT_MOTOR_PIN2 15
#define MAX_DISTANCE 200

NewPing sonar(TRIG_PIN, ECHO_PIN, MAX_DISTANCE);

void setup() {
  pinMode(LEFT_MOTOR_PIN1, OUTPUT);
  pinMode(LEFT_MOTOR_PIN2, OUTPUT);
  pinMode(RIGHT_MOTOR_PIN1, OUTPUT);
  pinMode(RIGHT_MOTOR_PIN2, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  if (sonar.ping_cm() < 20) {
    stopMovement();
    // Add logic for turning or recalculating path here
  } else {
    moveForward();
  }
  delay(100);
}

void moveForward() {
  digitalWrite(LEFT_MOTOR_PIN1, HIGH);
  digitalWrite(LEFT_MOTOR_PIN2, LOW);
  digitalWrite(RIGHT_MOTOR_PIN1, HIGH);
  digitalWrite(RIGHT_MOTOR_PIN2, LOW);
}

void stopMovement() {
  digitalWrite(LEFT_MOTOR_PIN1, LOW);
  digitalWrite(LEFT_MOTOR_PIN2, LOW);
  digitalWrite(RIGHT_MOTOR_PIN1, LOW);
  digitalWrite(RIGHT_MOTOR_PIN2, LOW);
}
