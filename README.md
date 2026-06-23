# smarthome-vsion-1.0
# SmartHome DIY

A Local-First Smart Home Platform built for makers, embedded developers, and DIY enthusiasts.

SmartHome DIY is a complete ecosystem including:

* Flutter Mobile App
* STM32 Master Gateway
* RF Smart End Devices
* RF Fixed Code Devices
* OpenBeken Devices
* MQTT Integration
* OTA Firmware Updates

The system is designed to be independent from cloud services, easy to repair, easy to customize, and affordable to build.

---

# Key Features

✅ Local-first architecture

✅ No cloud dependency

✅ Automatic LAN discovery

✅ MQTT support

✅ RF Fixed Code support (EV1527/PT2262 compatible)

✅ RF Smart Protocol

✅ OpenBeken integration

✅ OTA firmware update

✅ Remote device provisioning

✅ MQTT broker migration

✅ Multi-home support

✅ Room and device management

✅ Scene automation support

✅ Replace Master Gateway without re-pairing devices

---

# System Architecture

```text
                    Flutter App
                          |
                    MQTT / TCP
                          |
                 STM32 Master Gateway
                          |
    ------------------------------------------------
    |                     |                       |
RF Fixed Code       RF Smart Protocol       MQTT Devices
(EV1527/PT2262)      (CH32V003)             (OpenBeken)
```

---

# Design Philosophy

The system follows a Local-First design.

User data is stored inside the mobile application.

The Master Gateway acts primarily as a communication bridge between the application and devices.

Benefits:

* Easy gateway replacement
* No cloud lock-in
* Fast local control
* Low hardware cost
* Full ownership of devices
* Easy system recovery

---

# Supported Technologies

## RF Fixed Code

Compatible with common 433MHz devices:

* EV1527
* PT2262
* SC226x family
* Learning remote controls
* Wireless doorbells
* RF power sockets

Features:

* Learn code
* Store code
* Replay code

---

## RF Smart Protocol

Custom protocol developed specifically for SmartHome DIY.

Features:

* Device identification using DeviceKey
* Device status feedback
* Remote configuration
* OTA firmware updates
* Sensor reporting
* Reliable packet delivery
* Extensible binary payload structure

---

## OpenBeken Devices

Supported platforms:

* BK7231N
* CB3S
* WB3S

Integration via MQTT.

This allows existing Tuya-based devices flashed with OpenBeken to join the SmartHome DIY ecosystem.

---

# Master Gateway

## Hardware

* STM32F103RCT6
* W5500 Ethernet Controller
* RF 433MHz Module

## Responsibilities

* MQTT ↔ RF Gateway
* TCP ↔ RF Gateway
* Device Discovery
* OTA Transport
* Packet Forwarding

The Master Gateway does not store:

* Home information
* Room information
* Device names
* User accounts

This architecture allows easy replacement of the gateway without rebuilding the system.

---

# End Devices

Supported MCU:

* CH32V003F4P6

Examples:

* Smart Switch
* Smart Fan Controller
* Temperature Sensor
* Curtain Controller
* Custom Devices

Every device owns a unique DeviceKey.

Example:

```text
DeviceKey = 1001
```

---

# Communication Model

The system uses DeviceKey-based routing.

Example:

```text
DeviceKey = 1001
Payload   = Raw Binary Data
```

The gateway forwards packets without interpreting payload contents.

This allows developers to define custom payload structures for different device types.

Examples:

* Fan control packets
* Sensor packets
* Configuration packets
* OTA packets
* MQTT configuration packets

---

# Remote Device Provisioning

Devices can be configured remotely from the mobile application.

Example configurable parameters:

* MQTT Domain
* MQTT Port
* Username
* Password
* Device ID
* Default Topic

No firmware recompilation required.

No USB cable required.

---

# MQTT Broker Migration

Devices can migrate to a new MQTT server remotely.

Workflow:

1. User updates MQTT settings in the App
2. Configuration packet is sent to the device
3. Device validates CRC
4. Device stores new configuration
5. Device reconnects to the new broker

---

# OTA Firmware Update

OTA process:

1. Firmware download
2. Store image in external SPI Flash
3. Verify CRC
4. Bootloader performs upgrade
5. Remove temporary image after success

Benefits:

* Safe update process
* Recovery support
* Reduced risk of firmware corruption

---

# Mobile Application

Built using Flutter.

Features:

* Multi-user support
* Multi-home support
* Room management
* Device management
* Scene management
* MQTT integration
* LAN device discovery
* Local database using Hive

---

# Example Projects

* Smart Switch
* Smart Fan Controller
* Temperature Sensor
* RF Remote Controller
* OpenBeken Device Integration

---

# Why SmartHome DIY?

Many DIY solutions require:

* Cloud services
* Vendor lock-in
* Complex setup
* Expensive hardware

SmartHome DIY focuses on:

* Local control
* Low-cost hardware
* Easy customization
* Hardware ownership
* Educational value for embedded developers

---

# Project Goals

* Build a complete DIY Smart Home ecosystem
* Support low-cost hardware platforms
* Provide a flexible device framework
* Encourage community-driven development
* Help makers learn embedded systems, networking, and IoT technologies

---

# License

See LICENSE file for details.
