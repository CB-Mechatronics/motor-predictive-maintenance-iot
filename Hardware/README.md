# Hardware Documentation/ Documentación de Hardware.
These section contains the electronic design of the monitoring sistem, focusing on the adquisition of analog current readings and digital temperature and vibration data

_Esta sección contiene el diseño electrónico del sistema de monitoreo, enfocándose en la adquisición de datos analógicos de corriente y datos digitales de temperatura y vibracion_

### List of Materials / Lista de Materiales

| Component / Componente | Function / Función | Description / Descripción |
| :--- | :--- | :--- |
| **ESP32 DevKit** | MCU / Cerebro | Data processing and transmission via Wi-Fi (using MQTT). / Procesamiento y envío de datos vía Wi-Fi (usando MQTT). |
| **ADS1115 (x3)** | ADC / Convertidor | 16-bit resolution for current monitoring. / Resolución de 16 bits para monitoreo de corriente. |
| **MPU6050** | IMU / Inercial | Vibration and tilt analysis. / Análisis de vibración e inclinación. |
| **DS18B20** | Temp Sensor | Digital thermometer for motor case. / Termómetro digital para la carcasa del motor. |
| **SCT-013-000** | CT Sensor | Non-invasive current measurement. / Medición de corriente no invasiva. |
| **HLK-PM01** | Power Supply | AC 110/220V to DC 5V converter. / Convertidor de AC 110/220V a DC 5V. |
| **AMS1117** | Voltage Regulator | DC 5V to DC 3.3V converter. / Convertidor de DC 5V a DC 3.3V. |

The system integrates multiple sensors through standard industrial protocols to ensure data integrity:

Current (I2C): 3x ADS1115 (16-bit) connected to SCT-013 sensors for three-phase monitoring.

Vibration (I2C): MPU6050 accelerometer for spectral analysis of motor bearings.

Temperature (One-Wire): DS18B20 digital sensor for motor housing thermal monitoring.

_El sistema integra múltiples sensores a través de protocolos industriales estándar para garantizar la integridad de los datos:_

_Corriente (I2C): 3 ADS1115 (16 bits) conectados a sensores SCT-013 para monitoreo trifásico._

_Vibración (I2C): Acelerómetro MPU6050 para análisis espectral de los rodamientos del motor._

_Temperatura (One-Wire): Sensor digital DS18B20 para el monitoreo térmico de la carcasa._
