# Motor-predictive-maintenance-iot
IoT system for predictive maintenance in industrial induction motors using ESP32, Python, and Machine Learning.

# Predictive Maintenance System for Industrial Motors via IoT & AI
### *Sistema de Mantenimiento Predictivo para Motores Industriales mediante IoT e IA*

## Project Overview / Resumen del Proyecto
This project focuses on the development of a low-cost, professional-grade monitoring system for industrial motors. Using an **ESP32**, we capture vibration, temperature and current signatures to feed a **Machine Learning** model (Python) that predicts mechanical or electrical failures before they occur.

*Este proyecto se enfoca en el desarrollo de un sistema de monitoreo profesional de bajo costo para motores industriales. Utilizando un **ESP32**, capturamos firmas de vibración y corriente para alimentar un modelo de **Machine Learning** (Python) que predice fallas mecánicas o eléctricas antes de que ocurran.*

## Tech Stack / Tecnologías Utilizadas
* **Hardware:** ESP32, MPU6050 (Vibration), SCT-013 (Current), DS18B20 (Temperature).
* **Design:** AutoCAD (Installation Layouts), EasyEDA (PCB Design).
* **Software & AI:** Python (Scikit-Learn), Node-RED, MQTT.
* **Alerts:** Telegram Bot API.
  
# Predictive Monitoring System for Three-Phase Motors - Hardware Module v1.0
### Sistema de Monitoreo Predictivo para Motores Trifásicos - Módulo de Hardware v1.0

This repository contains the dual-layer printed circuit board (PCB) design optimized for high-precision data acquisition in predictive monitoring and fault diagnosis systems for industrial three-phase electric motors. The system utilizes an ESP32 microcontroller as the central processing unit and IoT gateway.

*Este repositorio contiene el diseño del circuito impreso (PCB) de doble capa optimizado para la adquisición de datos de alta precisión en sistemas de monitoreo predictivo y diagnóstico de fallas en motores eléctricos industriales de tres fases. El sistema utiliza un microcontrolador ESP32 como unidad central de procesamiento y conectividad IoT.*

---

## Technical Specifications / Especificaciones Técnicas del Hardware

The design has been thoroughly verified through Design Rule Checking (DRC) achieving **0 errors**, ensuring industrial manufacturability and high tolerance to severe electromagnetic interference (EMI) typical of electric machinery environments.

*El diseño ha sido verificado exhaustivamente mediante el análisis de Reglas de Diseño (DRC) obteniendo **0 errores**, garantizando su fabricabilidad industrial y una alta tolerancia al ruido electromagnético severo (EMI) característico de entornos con maquinaria eléctrica.*

| Parameter / Component <br> *(Parámetro / Componente)* | Board Configuration <br> *(Configuración en Placa)* | Technical Description <br> *(Descripción Técnica)* |
| :--- | :--- | :--- |
| **Main MCU** | ESP32-WROOM-32D | *Local processing, TCP/IP network stack, and native MQTT / Node-RED communication.* <br> Procesamiento local, gestión de red TCP/IP y comunicación nativa MQTT / Node-RED. |
| **A/D Conversion <br> *(Conversión A/D)*** | 3x ADS1115 (16-bit) | *Triple setup for simultaneous and independent analog sampling per motor phase.* <br> Triple configuración para el muestreo analógico simultáneo e independiente por cada fase del motor. |
| **Data Bus <br> *(Bus de Datos)*** | I2C (SDA / SCL) | *Balanced routing with continuous ground plane (GND) to prevent signal attenuation.* <br> Enrutamiento balanceado con plano de masa (*GND*) continuo para evitar atenuación de señal. |
| **Signal Conditioning <br> *(Acondicionamiento de Señal)*** | RC Low-Pass Filter <br> *(Filtro Pasa-Bajas RC)* | *Individual passive R/C network per analog channel to mitigate sensor harmonic noise.* <br> Red pasiva (R/C) individual por canal analógico para mitigar el ruido armónico de los sensores. |
| **Sensor Inputs <br> *(Entradas de Sensores)*** | KF2EDGK-5.08-2P Terminals | *Pluggable terminal blocks with 5.08 mm pitch for secure field connections.* <br> Bloques de terminales enchufables de paso de 5.08 mm para conexiones seguras en campo. |
| **Inertial Sensor <br> *(Sensor Inercial)*** | MPU-6050 (Isolated) | *Footprint optimized using a copper keepout zone (Prohibited Region) to prevent slot conflicts.* <br> Huella optimizada mediante zona de exclusión de cobre (*Prohibited Region*) para prevenir fallas por slots. |
| **Mechanical Fastening <br> *(Fijación Mecánica)*** | 4x M3 Holes (3.2 mm) | *Pure non-plated mechanical holes with full perimeter copper clearance.* <br> Perforaciones mecánicas puras no metalizadas (*Non-Plated*) con aislamiento perimetral completo. |

---

## Critical Engineering Considerations / Consideraciones Críticas de Ingeniería

### 🇺🇸 English
1. **Electromagnetic Noise Immunity:** Full flooded ground planes were implemented on both layers (*Top and Bottom Layer*), strategically interconnected using via stitching to shield the digital I2C bus against high-frequency interference induced by the motor.
2. **Analog Signal Integrity:** Traces for sensitive analog signals traveling from the input terminal blocks to the ADC pins were routed short, direct, and strictly confined to the *Top Layer*, minimizing parasitic inductance prior to digitization.
3. **Trace Width Optimization:** Traces handling power delivery and sensor supply voltages were designed with calculated widths to ensure adequate current-carrying capacity, minimizing thermal dissipation and voltage drops.
4. **Mechanical Safety and Assembly:** The M3 mounting holes feature a 3.2 mm cutting diameter and respect a copper-free clearance radius of over 3.5 mm. This prevents accidental short circuits or mechanical fractures in the FR-4 substrate when tightening metallic fasteners onto the chassis or enclosure.

### 🇪🇸 Español
1. **Inmunidad al Ruido Electromagnético:** Se implementaron planos de masa completos inundados en ambas capas (*Top y Bottom Layer*), interconectados estratégicamente mediante vías de costura (*via stitching*) para blindar el bus digital I2C contra interferencias de alta frecuencia inducidas por el motor.
2. **Integridad de Señales Analógicas:** Las pistas correspondientes a las señales delicadas que viajan desde las borneras de entrada hasta los pines analógicos de los ADC se ruteron de forma corta, directa y confinadas estrictamente en la capa superior (*Top Layer*), reduciendo la inductancia parásita antes de la digitalización.
3. **Optimización del Ancho de Pistas:** Las pistas encargadas de la distribución de potencia y voltajes de alimentación de los sensores se diseñaron con anchos calculados para asegurar una adecuada capacidad de conducción de corriente, minimizando la disipación térmica y las caídas de voltaje.
4. **Seguridad Mecánica y Ensamblaje:** Los agujeros de montaje M3 poseen un diámetro real de corte de 3.2 mm y respetan un radio libre de cobre (*clearance*) de más de 3.5 mm a la redonda. Esto previene cortocircuitos accidentales o grietas mecánicas en el sustrato FR-4 al ajustar la tornillería metálica sobre el chasis o gabinete.
   


---

## 📁 Repository Structure / Estructura del Repositorio

```text
├── Hardware/
│   ├── Gerber_motor_predictive_v1.0.zip   # Production-ready Gerber files / Archivos Gerber listos para manufactura
│   ├── Schematic_motor_predictive.pdf     # Circuit schematic diagram in PDF / Diagrama esquemático en PDF
│   └── Images/                            # Screenshots and 3D renders / Capturas y renders 3D de la placa
└── README.md                              # Main documentation / Documentación principal
