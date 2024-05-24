# Resistive_sensor
# Analog Sensor Data Averaging and Resistance Calculation
This Arduino project reads analog inputs from two pins (A0 and A1), calculates the average voltage, and computes the resistance based on the measured voltage. The results are printed to the serial monitor for easy observation.
# Overview
This project samples analog readings from two pins, A0 and A1, averages the readings over 20 samples, and then calculates the difference in voltage (Vout) and the sensor resistance (Rs). The results are output to the serial monitor.

# Components
Arduino board (e.g., Uno, Mega)
Analog sensors connected to A0 and A1
1k ohm resistor
# Code Explanation
# Setup
The setup() function initializes serial communication at 9600 bits per second.

void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
}
# Loop
The loop() function continuously reads analog inputs, computes the average voltage, and calculates the sensor resistance.
void loop() {
  long sumA1 = 0;
  long sumA0 = 0;
  int samples = 20;

  for (int i = 0; i < samples; i++) {
    sumA1 += analogRead(A1);
    sumA0 += analogRead(A0);
    delay(10); // Short delay to allow ADC to settle
  }

  float averageA1 = (sumA1 / (float)samples) / 1023.0 * 5.0;
  float averageA0 = (sumA0 / (float)samples) / 1023.0 * 5.0;
  float vout = abs(averageA1 - averageA0); // convert the voltage to milivolt
  float rs = (averageA1 * 115 ) / (5 - averageA1); // Assume the 1k ohm resistor

  Serial.println(rs, 2);
  delay(100); 
}
# Key Calculations

Averaging Analog Readings:
float averageA1 = (sumA1 / (float)samples) / 1023.0 * 5.0;
float averageA0 = (sumA0 / (float)samples) / 1023.0 * 5.0;

The analog readings are summed and averaged over the number of samples. The result is scaled to voltage.

Voltage Difference (Vout):
float vout = abs(averageA1 - averageA0);
The difference between the averaged voltages of A1 and A0.

Sensor Resistance (Rs):
float rs = (averageA1 * 115 ) / (5 - averageA1);

# Usage
Connect your sensors to the Arduino pins A0 and A1.
Upload the code to the Arduino.
Open the serial monitor to view the sensor resistance values.
# License
This project is licensed under the MIT License - see the LICENSE file for details.







