_**ESP32**_
The following code uses libraries such as Dallas temperature, OneWire and sensor to read the entry signals from the MPU6050 and the DS1115. The first prototype was built on Wokwi for ESP32 simulation. The absent of the SCT current sensor on the Wokwi's interface force me to mock the current signals until future improvements.
*El siguiente codigo usa la librerias de Dallas temperature, One Wire y sensor para leer señales de entrada del MPU6050 y el sensor de tmeperatura. El primer prototipo fue construido en Wokwi para simulacion de ESP32. La*
#include <Wire.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <OneWire.h>
#include <DallasTemperature.h>

// Configuración del sensor de temperatura DS18B20
#define ONE_WIRE_BUS 4
OneWire oneWire(ONE_WIRE_BUS);
DallasTemperature sensors(&oneWire);

Adafruit_MPU6050 mpu;

// Parámetros globales para la simulación de corriente (Ecuador: 60Hz)
const float FREQUENCY = 60.0;             
const float AMPLITUDE = 15.0;             
const float PHASE_B_SHIFT = 2.0943951;  // 120° en radianes
const float PHASE_C_SHIFT = 4.1887902;  // 240° en radianes

// ==========================================
// FUNCIÓN PARA SIMULAR LA LECTURA DEL ADS1115
// ==========================================
float readSimulatedCurrent(float time, float phaseShift) {
  float noise = (random(-20, 20) / 100.0); 
  return AMPLITUDE * sin(2.0 * PI * FREQUENCY * time - phaseShift) + noise;
}

void setup() {
  Serial.begin(115200);
  delay(1000);
  Serial.println("--- Starting Motor Predictive Monitoring Simulation ---");

  pinMode(ONE_WIRE_BUS, INPUT_PULLUP);

  if (!mpu.begin()) {
    Serial.println("Error: Could not find MPU-6050 chip.");
  } else {
    Serial.println("MPU-6050 Initialized.");
    mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  }

  sensors.begin();
  Serial.println("DS18B20 Initialized.");
}

void loop() {
  // 1. --- LECTURA DE VIBRACIÓN ---
  sensors_event_t a, g, temp_mpu;
  mpu.getEvent(&a, &g, &temp_mpu);

  // 2. --- LECTURA DE TEMPERATURA ---
  sensors.requestTemperatures(); 
  float motorTemp = sensors.getTempCByIndex(0);

  // 3. --- LECTURA DE CORRIENTES (Llamando a nuestra función modular) ---
  float t = millis() / 1000.0; // Tiempo actual en segundos
  
  float currentA = readSimulatedCurrent(t, 0.0);           // Fase A (0°)
  float currentB = readSimulatedCurrent(t, PHASE_B_SHIFT); // Fase B (120°)
  float currentC = readSimulatedCurrent(t, PHASE_C_SHIFT); // Fase C (240°)

  // 4. --- IMPRESIÓN DE DATOS Y ALERTAS ---
  
  // Monitoreo de Vibración
  Serial.print("[VIBRATION] X: "); Serial.print(a.acceleration.x, 2);
  Serial.print(" | Y: "); Serial.print(a.acceleration.y, 2);
  Serial.print(" | Z: "); Serial.print(a.acceleration.z, 2);
  Serial.println(" m/s^2");

  // Monitoreo de Temperatura y Alerta
  Serial.print("[TEMPERATURE] Motor Case: ");
  if (motorTemp == DEVICE_DISCONNECTED_C || motorTemp == -127.00) {
    Serial.println("Error de lectura.");
  } else {
    Serial.print(motorTemp, 2); Serial.println(" °C");
    if (motorTemp >= 50.0) {
      Serial.println("[ALERT] WARNING: Motor overheating detected!");
    }
  }

  // Monitoreo de Corriente Trifásica
  Serial.print("[CURRENT] Phase A: "); Serial.print(currentA, 2);
  Serial.print(" A | Phase B: "); Serial.print(currentB, 2);
  Serial.print(" A | Phase C: "); Serial.print(currentC, 2);
  Serial.println(" A");

  Serial.println("-----------------------------------------------------");
  delay(1000); // Muestreo cada segundo para el monitor
}
