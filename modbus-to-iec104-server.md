# Modbus to IEC104 Gateway: Configure EM300 as an IEC104 Server for SCADA Integration

Many industrial devices, such as energy meters, PLCs, and RTUs, still use Modbus RTU or Modbus TCP for field communication. However, power automation systems and SCADA platforms often require IEC 60870-5-104 communication.

Replacing existing Modbus devices is expensive and unnecessary. An industrial edge gateway can work as an IEC104 Server, collecting Modbus data and exposing standardized IEC104 points to SCADA systems.

---

## The Problem: Why Modbus Devices Cannot Talk to IEC104 Systems

In power automation and industrial control projects, numerous field devices—such as power meters, PLCs, sensors, and Remote Terminal Units (RTUs)—communicate via the Modbus protocol.

Meanwhile, control centers, SCADA systems, and Energy Management Systems (EMS) typically support the IEC 60870-5-104 protocol.

These two industrial communication protocols differ fundamentally in their data models, message structures, and communication mechanisms, making direct interoperability impossible.

### Core Differences at a Glance

| Feature | Modbus RTU/TCP | IEC 60870-5-104 |
| --- | --- | --- |
| Layer | Field/device level | SCADA/control center level |
| Primary Use | Device-to-device communication | Power system telecontrol |
| Protocol Type | Simple master-slave | Advanced telecontrol protocol with time-tagging |
| Transport | Serial (RTU) or TCP/IP | TCP/IP |
| Data Model | Register addresses (4x, 3x, etc.) | Information Object Addresses (IOA) |
| Key Features | Simple, widely adopted | Clock synchronization, event reporting, command confirmation |

Without a protocol conversion gateway, Modbus field devices cannot be understood by IEC104 control centers, creating an integration bottleneck in substation automation systems and smart grid projects.

---

## The Solution: EM300 Modbus to IEC104 Gateway

![EM300 edge controller - Modbus to IEC104 gateway](https://en.iotrouter.com/wp-content/uploads/2026/07/EM300-edge-controller.webp)

The EM300 Modbus to IEC104 Gateway is designed to simplify industrial protocol integration by overcoming the limitations of traditional gateways, including fixed I/O, separated control systems, complex application development, and high remote maintenance costs.

It integrates six core capabilities into a single device:

- Edge computing
- Visual programming
- Protocol conversion
- Industrial protocols
- Industrial networking
- Scalable I/O

Beyond Modbus-to-IEC104 conversion, the EM300 supports flexible IEC 60870-5-104 communication roles.

It can operate as an **IEC104 Server (slave/remote station)** to provide field data to SCADA systems, dispatch centers, and Energy Management Systems (EMS), or as an **IEC104 Client (master)** to communicate with IEC104-compatible devices and systems.

In a typical Modbus-to-IEC104 application, the EM300 collects data from Modbus RTU/TCP devices on the field side and maps the acquired variables to IEC104 information objects through its built-in IEC104 Server node.

The converted data can then be accessed by IEC104 clients, enabling existing Modbus devices to integrate with power automation and SCADA infrastructures.

---

## Step 1: Prepare the Gateway and Field Data

Before configuring the IEC104 Server, make sure the required data points and communication environment are ready.

### 1.1 Preparation Requirements

Confirm the data points that need to be collected and uploaded to the IEC104 system, including:

- Tele-signaling points
- Telemetry points
- Tele-control points
- Tele-regulation points

Connect the industrial gateway to the same local network as the IEC104 client or host system.

### Typical Communication Architecture

```text
Field Devices
(Modbus RTU/TCP)
        ↓
EM300 Industrial Edge Controller
        ↓
IEC104 Server
        ↓
SCADA / IEC104 Client
```

### 1.2 Connect the Gateway

For detailed connection instructions, see:

[How to Connect the EM Series Edge Controller](https://en.iotrouter.com/how-to-connect-the-em-series-edge-controller/)

---

## Step 2: Open the Visual Programming Interface

After completing the gateway network configuration, enter the **Visual Programming** interface.

Click the **NODE-RED** button in the top-right corner of the page.

![Open the EM300 Node-RED visual programming interface](https://en.iotrouter.com/wp-content/uploads/2026/07/image1-1200x615.png)

Add the **IEC104 Server node** and configure the required communication parameters and point table.

---

## Step 3: Configure the IEC104 Server Node

Select the IEC104 Server node, then configure the required parameters and point mappings.

![IEC104 Server node configuration - part 1](https://en.iotrouter.com/wp-content/uploads/2026/07/2-1_1_11zon.webp)

![IEC104 Server node configuration - part 2](https://en.iotrouter.com/wp-content/uploads/2026/07/2-2_2_11zon.webp)

---

## Step 4: Deploy and Test

### Inject – Write Data

![IEC104 Server inject write data test](https://en.iotrouter.com/wp-content/uploads/2026/07/3-1_3_11zon.webp)

### View Output

![IEC104 Server output test](https://en.iotrouter.com/wp-content/uploads/2026/07/3-2_4_11zon.webp)

---

# IEC104 Server Node Configuration Reference

## 1. Configuration Parameters

| Parameter | Description |
| --- | --- |
| Name | The name displayed for the node in the flow. |
| Port | The listening port of the IEC104 server. |
| t0 | Timeout for establishing a connection. Unit: seconds. |
| t1 | Timeout for sending or testing APDU frames. Unit: seconds. |
| t2 | Timeout for acknowledgement when no data messages are received. Unit: seconds. `t2 < t1` |
| t3 | Idle timeout for sending test frames. Unit: seconds. `t3 > t1` |
| k | Maximum number of unacknowledged `[I]` frames allowed before the sender disconnects the connection. |
| w | Number of received messages before the receiver sends an `[S]` frame acknowledgement. |
| Mode | Server/Slave mode. `Connection is Redundant Group` supports multiple connections. |
| Periodic Report | Data points with the `Periodic` option enabled will periodically report telemetry and status data to the IEC104 client according to this interval. |
| Spontaneous Report | Supports reporting triggered by value changes, parameter updates, and quality changes. |
| Log (Debug Only) | Used only for debugging purposes. |
| Remote Control/Adjustment Output Value Only | When enabled, only the value of remote control and adjustment commands is output. Otherwise, the output is in array format. |

---

## 2. Point Table

The point table can be used to quickly update the telemetry and status data of the IEC104 server (slave).

| Field | Description |
| --- | --- |
| IOA (Information Object Address) | The data point address stored in the server (slave). |
| COA (Common Address) | The common address of the IEC104 station. |
| Name | A custom name for the data point. It cannot be empty and must be unique. The name is used as the output key. Example: `msg.payload.a = true`, where `a` is the custom name. |
| Type | Data point type. |

### Notes

- The IOA address can be duplicated, but the data type must be the same.

For example, if:

```text
ioa=1, type=1
```

already exists in the point table, adding:

```text
ioa=1, type=2
```

will cause an error.

If the configuration is forcibly saved, the server will discard the data point:

```text
ioa=1, type=2
```

- The IEC104 server (slave) only stores remote control and remote adjustment points. It does not store command values.
- Clock synchronization is supported.

---

## 3. Input

The node supports inputting point values in the following formats:

- Number
- Array

When Array format is used, the server parses the values according to the array order.

---

## Write Examples

```javascript
msg.payload.a = 0
```

or:

```javascript
msg.payload.a = "1,0,0,0,0"
```

or:

```javascript
msg.payload.a = [1,0,0,0,0]
```

---

## Read Examples

```javascript
msg.payload.a = null
```

or:

```javascript
msg.payload.a = [null,null,null,null,null]
```

---

# Why Choose EM300 as a Modbus to IEC104 Gateway

## 1. All-in-One Integration

The EM300 integrates six core functions:

- Edge computing
- Visual programming
- Protocol conversion
- Industrial protocols
- Industrial routing
- Scalable I/O

One unit can handle protocol conversion, data acquisition, remote operations, and I/O control, reducing the need for separate PLCs, routers, or industrial PCs.

---

## 2. Node-RED Visual Programming

The EM300 provides a deeply customized Node-RED visual programming tool.

The acquisition, transmission, and control workflow can be configured through visual nodes, reducing the need for conventional PLC or industrial PC programming for these integration tasks.

---

## 3. Industrial Protocol Library

The EM300 includes support for industrial and power communication protocols such as:

- Modbus RTU/TCP
- OPC UA
- BACnet
- IEC104
- IEC61850*
- DL/T645
- HJ212
- CJ188

These protocols can be used to integrate devices such as power meters, PLCs, and smart electricity meters.

---

## 4. Industrial-Grade Reliability

The EM300 is designed for industrial environments with an operating temperature range of:

```text
-40°C to 85°C
```

It includes hardware watchdog protection and supports:

- Automatic reconnection after network failure
- Intelligent data retransmission
- Optional UPS power failure protection
- Data buffering
- Parameter snapshots
- Safe shutdown

---

## 5. Flexible I/O Expansion

The EM300 includes:

```text
4 × isolated RS485
2 × isolated DI
2 × isolated DO
```

It supports up to **16 I/O expansion modules**, including:

- Digital input modules
- Digital output modules
- Relay output modules
- Analog input modules
- Analog output modules

The distributed I/O architecture supports millisecond-level control response.

---

## 6. Remote Operations

With IOTRouter's remote operations software **IOTClient**, the EM300 supports:

- Remote configuration
- Remote debugging
- Remote diagnostics
- Remote firmware updates
- VPN
- Firewall
- Cross-site device networking
- Intranet penetration
- P2P direct connection

---

## 7. Flexible Data Read/Write Methods

The EM300 supports both:

- K-V key-value pair data read/write
- Object injection data read/write

It also supports IEC104 functions including:

- General interrogation
- Clock synchronization

---

# FAQ

## Can Modbus devices directly connect to IEC104 systems?

No.

Modbus and IEC104 are fundamentally different industrial communication protocols with different data models, message structures, and communication mechanisms.

A protocol conversion gateway such as the EM300 is required to enable interoperability.

---

## What is a Modbus to IEC104 gateway?

A Modbus to IEC104 gateway is an industrial protocol conversion device that acquires data from Modbus RTU/TCP devices and converts it to IEC 60870-5-104 format.

The converted data can then be used by:

- SCADA systems
- Dispatch centers
- Energy Management Systems (EMS)
- Power monitoring platforms

---

## Does IEC104 support TCP/IP?

Yes.

IEC 60870-5-104 is designed as a telecontrol protocol for TCP/IP networks and is suitable for Ethernet-based SCADA and dispatch center communications.

---

## What is the default port for IEC104?

The default TCP port for IEC 60870-5-104 is:

```text
2404
```

This is also the port used by the EM300 IEC104 Server node by default.

---

## Does EM300 support both periodic and spontaneous reporting?

Yes.

The EM300 IEC104 Server node supports:

- Periodic reporting
- Spontaneous reporting triggered by data changes
- Parameter update reporting
- Quality-change reporting

---

## What industries use Modbus to IEC104 conversion?

Typical applications include:

- Power generation
- Power transmission and distribution
- Substation automation
- Renewable energy systems
- Solar and wind power
- Smart grids
- Factory power management
- Building Energy Management Systems (EMS)

---

# Summary

A typical Modbus-to-IEC104 deployment with EM300 consists of three main steps:

1. Connect Modbus devices.
2. Configure the IEC104 Server point table.
3. Deploy and test the communication flow.

The EM300 then bridges Modbus RTU/TCP field devices with IEC104-compatible power automation and SCADA systems.

---

## Related Guide

For the complete illustrated article and additional background information, see:

[Modbus to IEC104 Gateway Setup Guide](https://en.iotrouter.com/modbus-to-iec-104-gateway-setup-guide/)

For initial device connection and login instructions, see:

[How to Connect the EM Series Edge Controller](https://en.iotrouter.com/how-to-connect-the-em-series-edge-controller/)
