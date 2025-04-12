// Sensor Pins
#define SENSOR_LEFT  4   
#define SENSOR_MID   3   
#define SENSOR_RIGHT 2   

// Motor Driver Pins (L298N)
#define enA 10  // Left motor speed control (PWM)
#define in1 9   // Left motor forward
#define in2 8   // Left motor backward
#define in3 7   // Right motor forward
#define in4 6   // Right motor backward
#define enB 5   // Right motor speed control (PWM)

// Ultrasonic Sensor Pins
#define TRIG_PIN A3
#define ECHO_PIN A2
#define OBSTACLE_DISTANCE 15 // Distance threshold in cm

void setup() {
    Serial.begin(9600);

    // Sensor pins as input
    pinMode(SENSOR_LEFT, INPUT);
    pinMode(SENSOR_MID, INPUT);
    pinMode(SENSOR_RIGHT, INPUT);

    // Motor pins as output
    pinMode(enA, OUTPUT);
    pinMode(in1, OUTPUT);
    pinMode(in2, OUTPUT);
    pinMode(in3, OUTPUT);
    pinMode(in4, OUTPUT);
    pinMode(enB, OUTPUT);

    // Ultrasonic Sensor Pins
    pinMode(TRIG_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);

    // Set default motor speed
    analogWrite(enA, 220); // Adjust speed (0-255)
    analogWrite(enB, 220);
}

void loop() {
    // Check for obstacles
    if (detectObstacle()) {
        stopMotors();
        Serial.println("Obstacle detected! Stopping...");
        while (detectObstacle()) {
            delay(100); // Keep checking for obstacle removal
        }
        Serial.println("Obstacle removed! Resuming path...");
    }

    // Read sensor values
    int left = digitalRead(SENSOR_LEFT);
    int mid = digitalRead(SENSOR_MID);
    int right = digitalRead(SENSOR_RIGHT);

    Serial.print("L: "); Serial.print(left);
    Serial.print(" | M: "); Serial.print(mid);
    Serial.print(" | R: "); Serial.println(right);

    // Line following logic
    if (left == 0 && mid == 1 && right == 0) {
        moveForward();  // Move straight
    } 
    else if (left == 1 && mid == 1 && right == 0) {
        turnLeft();  // Rotate left until L0 M1 R0
    } 
    else if (left == 0 && mid == 1 && right == 1) {
        turnRight();  // Rotate right until L0 M1 R0
    } 
    else if (left == 1 && mid == 0 && right == 0) {
        turnLeft();  // Slightly rotate left
    } 
    else if (left == 0 && mid == 0 && right == 1) {
        turnRight(); // Slightly rotate right
    } 
    else if (left == 0 && mid == 0 && right == 0) {
        stopMotors(); // Rotate left & right till middle detects line
    } 
    else if (left == 1 && mid == 1 && right == 1) {
        stopMotors(); // Stop if no valid input
    }

    delay(50);  // Short delay for sensor stability
}

// ========== Motor Control Functions ==========

void moveForward() {
    digitalWrite(in1, LOW);  
    digitalWrite(in2, HIGH);
    digitalWrite(in3, LOW);  
    digitalWrite(in4, HIGH);
}

void turnLeft() {
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);
}

void turnRight() {
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);
}

void stopMotors() {
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);
}

// ========== Ultrasonic Sensor Functions ==========

bool detectObstacle() {
    long duration;
    int distance;

    // Trigger the ultrasonic sensor
    digitalWrite(TRIG_PIN, LOW);
    delayMicroseconds(2);
    digitalWrite(TRIG_PIN, HIGH);
    delayMicroseconds(10);
    digitalWrite(TRIG_PIN, LOW);

    // Read the echo pin
    duration = pulseIn(ECHO_PIN, HIGH);
    distance = duration * 0.034 / 2; // Convert to cm

    Serial.print("Distance: ");
    Serial.print(distance);
    Serial.println(" cm");

    return (distance > 0 && distance < OBSTACLE_DISTANCE); // Returns true if obstacle is detected
}
