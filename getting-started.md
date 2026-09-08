# Getting Started with EM Series Edge Controllers

This guide explains how to connect an IOTRouter EM Series edge controller, access the web-based configuration interface, and check the basic device and network status.

The EM Series supports two local connection methods:

- Direct Ethernet connection through the LAN port
- Wireless connection through the built-in WiFi Access Point (AP) mode

After establishing the connection, the device management interface can be accessed through a web browser for basic configuration, status monitoring, and system management.

---

## 1. Connect the EM Series Edge Controller

### 1.1 Direct Ethernet Connection

Use an Ethernet cable to connect the computer network port to the **LAN port** of the EM Series edge controller.

The default LAN IP address is:

```text
192.168.88.1
```

Configure the computer's IP address to the same network segment.

Example:

```text
IP Address: 192.168.88.100
Subnet Mask: 255.255.255.0
```

After the network configuration is completed, open a web browser and enter:

```text
http://192.168.88.1
```

The login page will be displayed.

---

### 1.2 WiFi Connection (AP Mode)

The EM Series edge controller also supports wireless access through WiFi AP mode.

Use the computer's WiFi function to connect to the controller hotspot.

The default WiFi name is:

```text
EM300-XXXX
```

`XXXX` represents the last four digits of the device serial number (SN).

The default WiFi password is:

```text
EM12345678
```

After a successful connection, the computer will automatically obtain an IP address from the controller.

The default gateway IP address is:

```text
192.168.88.1
```

Open a web browser and enter the IP address to access the configuration interface.

---

## 2. Basic Configuration

### 2.1 Login Interface

After accessing the login page, use the default administrator account:

```text
Username: admin
Password: EM12345678
```

> **Security Notice:** After the first login, it is strongly recommended to change the default password to improve device security.

---

### 2.2 Dashboard Overview

After successful login, the dashboard displays:

- Basic device information
- Network status
- System load status
- External storage information

> **Note:** Different EM Series models may display different parameter items. The actual interface depends on the specific device model.

---

### 2.3 Device Information

The **Device Information** section displays the basic information of the edge controller.

#### Model

Displays the specific device model.

Example:

```text
EM300
```

#### SN

Displays the device serial number.

The SN is a globally unique identifier used for device identification and remote management.

#### Firmware Version

Displays the current firmware version installed on the device.

The displayed version depends on the actual firmware installed.

#### Device Status

Displays the current operating status of the device.

Examples:

- Running
- Offline
- Initializing

#### Network Type

Displays the current network connection method.

Available status options include:

- WAN
- 4G
- WiFi
- Unknown

`Unknown` indicates that the device is currently not connected to a network.

#### Remote Status

Displays the remote connection status.

#### Running Time

Displays the total operating time since the device was powered on.

#### Local Time

Displays the current system time of the device.

---

### 2.4 Network Information

The **Network Information** section displays the current network configuration and connection status.

It includes information such as:

- WAN network status
- 4G cellular network status
- WiFi status
- IP address
- MAC address
- Network connection information

The displayed parameters depend on the installed communication modules and network configuration.

---

## 3. Important Notes

1. Change the default password after the first login.

2. Make sure the computer and the EM Series controller are configured within the same IP network segment before accessing the web interface.

3. If the device cannot be accessed, check:

   - Ethernet cable connection
   - Computer IP configuration
   - Network adapter status
   - Device power supply

---

## 4. Next Steps

After completing the connection and login steps, the EM Series edge controller is ready for basic configuration and further application development.

According to application requirements, users can continue configuring:

- Communication interfaces
- Industrial protocols
- I/O modules
- Node-RED applications
- Other edge computing functions

---

## Full Illustrated Guide

For screenshots and the complete illustrated walkthrough, see:

[How to Connect the EM Series Edge Controller](https://en.iotrouter.com/how-to-connect-the-em-series-edge-controller/)
