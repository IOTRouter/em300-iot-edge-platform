# EM300 IEC 60870-5-104 Client Configuration Guide

## Overview

This guide explains how to configure the IOTRouter EM300 Modular Industrial Edge Controller as an IEC 60870-5-104 (IEC104) Client using its Node-RED visual programming environment.

In IEC104 Client mode, EM300 initiates a TCP connection to an IEC104 Server, receives monitoring data, performs general interrogation, and sends supported control commands.

This functionality is suitable for industrial power monitoring, renewable energy systems, substation automation, and IEC104 device integration.

**Hardware:** IOTRouter EM300 (FlowPLC)  
**Communication protocol:** IEC 60870-5-104  
**Operating mode:** IEC104 Client  
**Configuration environment:** Node-RED  
**Firmware version:** Confirm with your device documentation

## 1. IEC104 Client vs. IEC104 Server

IEC104 defines two communication roles:

| Feature | IEC104 Client | IEC104 Server |
|---|---|---|
| TCP Connection | Initiates connection | Accepts connection |
| Monitoring Data | Receives data | Provides data |
| General Interrogation | Sends requests | Responds to requests |
| Remote Control | Sends commands | Processes commands |
| Typical Application | IEC104 system integration | SCADA data provision |

EM300 supports both communication roles. Select the correct role based on the architecture of your industrial system.

## 2. System Architecture

Example IEC104 Client communication:

```text
+-------------------------+
|      IOTRouter EM300    |
|                         |
|    IEC104 Client Node   |
|        (Node-RED)       |
+------------+------------+
             |
             | TCP/IP
             | IEC 60870-5-104
             |
+------------v------------+
|       IEC104 Server     |
|                         |
| RTU / Substation Device |
|   Monitoring & Control  |
+-------------------------+
```

EM300 initiates a connection to the configured IEC104 Server and exchanges monitoring data and supported commands.

Other industrial devices can be integrated into EM300 workflows through supported protocols such as Modbus RTU/TCP. The specific data flow and mapping depend on the project architecture.

## 3. Requirements

Before configuration, prepare:

- An IOTRouter EM300 Edge Controller
- Access to the Node-RED configuration interface
- A reachable IEC104 Server
- The server IP address and TCP port
- IEC104 station address and point information
- Network connectivity between the client and server

The standard IEC104 TCP port is 2404, unless a different port has been configured on the server.

Ensure that the target server permits connections from EM300.

## 4. Configure EM300 as an IEC104 Client

### Step 1: Access Node-RED

1. Connect EM300 to the industrial network.
2. Open the device management interface.
3. Enter the Node-RED visual programming environment.
4. Create or open the required workflow.

### Step 2: Add the IEC104 Client Node

1. Locate the IEC104 Client node in the available Node-RED nodes.
2. Add the node to the workflow.
3. Open its configuration panel.
4. Enter the target IEC104 Server IP address and port.

Ensure that the server address and network settings match the actual deployment environment.

### Step 3: Configure Communication Parameters

The IEC104 Client node provides parameters for connection management and data exchange.

| Parameter | Description |
|---|---|
| Server IP | IP address of the target IEC104 Server |
| Port | IEC104 TCP port, normally 2404 |
| t0 | Connection establishment timeout |
| t1 | APDU send/test timeout |
| t2 | Delayed acknowledgement timeout |
| t3 | Idle link test interval |
| k | Maximum outstanding unacknowledged I-frames |
| w | Received I-frames threshold for acknowledgement |
| General Interrogation | Request process data after connection |
| Counter Interrogation | Request counter data after connection |
| Reconnection Time | Delay before attempting reconnection |

Configure the parameters according to the server requirements.

The timers and acknowledgement settings must be compatible with the IEC104 peer. In particular, t2 should be shorter than t1, and the receive acknowledgement configuration should be consistent with the peer's window settings.

### Step 4: Configure Data Points

Use the IEC104 point information supplied by the server system.

Common IEC104 data types include:

- Single-point information
- Double-point information
- Normalized measured values
- Scaled measured values
- Short floating-point measured values
- Integrated totals

Confirm the Common Address (CA/COA), Information Object Address (IOA), and data type for each point.

Incorrect address or type mappings may prevent correct data interpretation.

### Step 5: Configure Interrogation

Depending on the application, enable the required functions:

- General Interrogation after connection
- Counter Interrogation after connection
- Periodic interrogation
- Clock synchronization

These functions must also be supported and permitted by the target IEC104 Server.

### Step 6: Deploy the Workflow

1. Review the IEC104 Client configuration.
2. Deploy the Node-RED workflow.
3. Check the connection status.
4. Confirm that monitoring data is received correctly.

If the connection fails, verify the server address, port, firewall rules, and IEC104 communication parameters.

## 5. Remote Control and Commands

The EM300 IEC104 Client supports common command categories, including:

| Command Type | IEC104 Type ID |
|---|---|
| Single command | C_SC_NA_1 (45) |
| Double command | C_DC_NA_1 (46) |
| Regulating step command | C_RC_NA_1 (47) |
| Set-point command, normalized | C_SE_NA_1 (48) |
| Set-point command, scaled | C_SE_NB_1 (49) |
| Set-point command, short floating point | C_SE_NC_1 (50) |
| Bitstring of 32 bits | C_BO_NA_1 (51) |
| General interrogation | C_IC_NA_1 (100) |
| Counter interrogation | C_CI_NA_1 (101) |
| Clock synchronization | C_CS_NA_1 (103) |

Actual command availability and behavior depend on the firmware, node configuration, server implementation, and device permissions.

**Important:** Test remote control functions only on authorized systems or a controlled test environment. Avoid sending commands to live equipment without an approved commissioning procedure.

## 6. Testing and Verification

After deploying the workflow, verify the following functions.

| Test | Expected Result |
|---|---|
| TCP connection | EM300 establishes communication with the server |
| General interrogation | Server responds with supported monitoring data |
| Data point reading | Received data matches the server point table |
| Reconnection | Communication recovers according to configured settings |
| Remote control | Authorized test command receives the expected response |
| Clock synchronization | Server processes the request if supported |

These are recommended verification checks, not a report of completed tests.

For remote control testing, confirm both the IEC104 response and the actual state of the test point.

## 7. Troubleshooting

### Unable to Connect to the IEC104 Server

Check:

- Server IP address and TCP port
- Network routing and firewall rules
- IEC104 Server availability
- Connection timeout configuration
- Server connection limits

### Connected but No Monitoring Data

Check:

- Common Address (CA/COA)
- Information Object Address (IOA)
- General interrogation configuration
- Supported data types
- Server point table configuration

### Remote Control Command Fails

Check:

- Command type and IOA
- Command permissions
- Select-before-operate requirements, if applicable
- Server-side command handling
- IEC104 response and cause of transmission

## 8. Typical Applications

**Substation Monitoring**

Connect EM300 to IEC104 Server-enabled RTUs or substation equipment for monitoring data acquisition and integration.

**Renewable Energy Systems**

Communicate with IEC104-enabled energy devices and controllers in solar, storage, and distributed energy applications.

**Industrial Power Monitoring**

Collect monitoring data from compatible IEC104 systems and integrate it into industrial edge workflows.

## 9. Related Documentation

- [EM300 Overview](overview.md)
- [EM300 Product Specification](product_specification.md)
- [Modbus to IEC104 Server Configuration](modbus-to-iec104-server.md)
- [Getting Started with EM300](getting-started.md)

### Full Step-by-Step Tutorial

For configuration screenshots, detailed explanations, and an example of IEC104 command testing, refer to the official IOTRouter tutorial:

[IEC104 Client Gateway: Connect Industrial Devices to SCADA](https://en.iotrouter.com/iec104-client-gateway-connect-industrial-devices-to-scada-without-plc/)

## 10. About EM300

EM300 is a modular industrial edge controller developed by IOTRouter for industrial data acquisition, protocol integration, edge processing, and scalable I/O applications.

Key capabilities include:

- Node-RED visual programming
- IEC104 Client and Server communication
- Modbus RTU/TCP and other industrial protocols
- 4 isolated RS485 interfaces
- Ethernet and wireless connectivity
- Expandable industrial I/O modules
- Remote device management

**Official Product Page:**

[EM300 Modular Industrial Edge Controller](https://en.iotrouter.com/product/em300-modular-industrial-edge-controller/)

---

**Maintained by IOTRouter**

Technical documentation and integration resources for industrial IoT and edge computing.
