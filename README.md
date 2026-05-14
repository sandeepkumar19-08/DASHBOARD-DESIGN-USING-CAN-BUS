Dashboard Design Using CAN Bus

A CAN Bus based automotive dashboard system using the LPC2129 microcontroller to monitor and display engine temperature, fuel percentage, and vehicle indicator status.
This project demonstrates distributed embedded communication using the CAN Protocol with multiple nodes.


**📌 Project Overview**

This project is designed to simulate a basic automotive dashboard system where multiple nodes communicate through the CAN Bus network.

The system performs the following operations:

Displays Engine Temperature
Displays Fuel Percentage
Controls Left & Right Indicators
Displays RTC Information (Time, Date & Day)
Transfers sensor data between nodes using CAN Protocol


**🛠️ Hardware Requirements**
LPC2129 Microcontroller
MCP2551 CAN Transceiver
LCD Display
LEDs
Push Buttons / Switches
DS18B20 Temperature Sensor
Fuel Gauge Sensor / Potentiometer
USB to UART Converter


**💻 Software Requirements**
Embedded C
KEIL uVision Compiler
Flash Magic


**📚 Concepts Used**
Embedded C Programming
LPC2129 Architecture
GPIO Interface
ADC (Analog to Digital Converter)
CAN Communication Protocol
RTC Interface
External Interrupts
Sensor Interfacing


**🧩 System Architecture**

The project contains three CAN nodes:


**1️⃣ Main Node**

Responsible for:

Reading engine temperature
Displaying RTC details
Sending indicator commands
Receiving fuel information
Updating LCD display


**2️⃣ Indicator Node**

Responsible for:

Receiving CAN messages
Controlling Left/Right indicators using LEDs


**3️⃣ Fuel Node**

Responsible for:

Reading fuel sensor value using ADC
Sending fuel percentage data to Main Node


**🔄 Working Flow**
Temperature sensor data is read by the Main Node.
Fuel Node continuously reads fuel level and transmits via CAN.
Indicator switches generate interrupts.
Main Node sends indicator status through CAN.
Indicator Node activates corresponding LEDs.
LCD displays:
Engine Temperature
Fuel Percentage
Indicator Status
RTC Information


========================================================================
                 DASHBOARD DESIGN USING CAN BUS
                           COMPLETE FLOW
========================================================================


                                START
                                  │
                                  ▼
                    Power ON All CAN Nodes
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
          ▼                       ▼                        ▼


========================================================================
                           MAIN NODE FLOW
========================================================================

            Initialize Main Node Peripherals
            --------------------------------
            • LCD
            • RTC
            • CAN Controller
            • DS18B20 Temperature Sensor
            • External Interrupts
            • GPIO
                                  │
                                  ▼
                     Display Welcome Message
                                  │
                                  ▼

                         MAIN LOOP START
                                  │
                                  ▼
                 Read Engine Temperature Sensor
                                  │
                                  ▼
                      Read RTC Information
                    (TIME / DATE / DAY)
                                  │
                                  ▼
                     Display on LCD Screen
                     ---------------------
                     • Temperature
                     • Time
                     • Date
                     • Day
                     • Fuel Percentage
                     • Indicator Status
                                  │
                                  ▼
               Check Interrupt for Indicator Switch
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                   NO                          YES
                    │                           │
                    │                           ▼
                    │            Determine Indicator Status
                    │             • LEFT Indicator
                    │             • RIGHT Indicator
                    │             • OFF
                    │                           │
                    │                           ▼
                    │             Create CAN Data Frame
                    │                           │
                    │                           ▼
                    │          Send Indicator Command
                    │           to Indicator Node
                    │                           │
                    │                           ▼
                    │          Update Indicator Status
                    │                on LCD
                    │
                    ▼
           Check for Fuel Data from Fuel Node
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                   NO                          YES
                    │                           │
                    │                           ▼
                    │              Read CAN Fuel Data
                    │                           │
                    │                           ▼
                    │            Convert Data to Fuel %
                    │                           │
                    │                           ▼
                    │         Update Fuel % on LCD
                    │
                    ▼
                         Repeat Main Loop



========================================================================
                        INDICATOR NODE FLOW
========================================================================

              Initialize Indicator Node
              -------------------------
              • CAN Controller
              • GPIO
              • LED Outputs
                                  │
                                  ▼

                      INDICATOR LOOP START
                                  │
                                  ▼
                    Wait for CAN Message
                     from Main Node
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                   NO                          YES
                    │                           │
                    │                           ▼
                    │              Read CAN Message
                    │                           │
                    │                           ▼
                    │             Decode Indicator Data
                    │
                    │       ┌──────────┼──────────┐
                    │       │          │          │
                    │       ▼          ▼          ▼
                    │     LEFT       RIGHT       OFF
                    │       │          │          │
                    │       ▼          ▼          ▼
                    │  LEFT LED     RIGHT LED    BOTH LEDs
                    │     ON            ON          OFF
                    │ RIGHT LED     LEFT LED
                    │     OFF           OFF
                    │
                    ▼
                     Repeat Indicator Loop



========================================================================
                           FUEL NODE FLOW
========================================================================

                Initialize Fuel Node
                --------------------
                • ADC
                • CAN Controller
                • Fuel Sensor
                                  │
                                  ▼

                         FUEL LOOP START
                                  │
                                  ▼
                   Read Fuel Sensor using ADC
                                  │
                                  ▼
                    Convert ADC Value to %
                                  │
                                  ▼
                     Prepare CAN Data Frame
                                  │
                                  ▼
                 Send Fuel % to Main Node
                                  │
                                  ▼
                        Repeat Fuel Loop



========================================================================
                            FINAL OUTPUT
========================================================================

LCD DISPLAY:
-------------
• Engine Temperature
• Fuel Percentage
• Time
• Date
• Day
• Left Indicator Status
• Right Indicator Status


LED OUTPUT:
------------
• Left Indicator LED ON/OFF
• Right Indicator LED ON/OFF
