# Portable HART-IP v2.0 Client

With an installed base of over 40 million devices, the HART Communication Protocol is the leading protocol for smart process automation field devices.  HART-IP enables the communication of native binary HART data across the Internet allowing access to HART devices.  This complete HART IP Client example simplifies the development of applications using HART-IP to access and utilize HART field devices.

The HART-IP Client is an application that connects a host to HART devices using the HART-IP protocol.  Devices include: 
* I/O devices like Gateways and Multiplexers 
* Native HART-IP field devices

The user interface runs in a browser and is based on the Vue framework for web applications.

This Client enables the user to send HART commands to the connected HART-IP device and any sub-devices through the network connection.  The Client receives and displays the responses on its user interface.

This Readme describes how to build, deploy and use this example HART-IP 2.0 Client.  The Usage subsection includes example HART communications.  The data you actually will receive depends on the connected field device and process conditions captured by that device.

For more information, see the [wrong data sheet here](https://support.fieldcommgroup.org/helpdesk/attachments/8057534489).

## Features Included

1. Support for HART-IP, versions  1 and 2
2. Portable to Windows, Mac, and Linux
3. Browser-based user interface based on HTML5
4. Displays  Messages in a friendly, human-readable format
4. Example of TCP and UDP communication with a HART-IP 2.0 device.
2. Addressing sub-devices through an I/O device using HART-IP protocol.
3. A simple method of parsing HART binary messages using DeviceInfo files.
4. A REST API for web-oriented access to HART IP devices
6. Secure UDP and TCP connections with UDP/DTLS, TCP/TLS PSK (static PSK cipher) and SRP connections
7. A simple manager for security credentials
8. Direct PDU messages
9. Read audit logs

In addition, the phip supports a wide range of [HART Commands](doc/Portable%20HART-IP%20Commands.r1.md) 

## See the following for more information

- [1 Introduction to Portable HART-IP Client](doc/1-Intro.r1.md)
- [2 Overview of Portable HART-IP Client Operation](doc/2-Overview.r1.md)
- [3 Connecting to the HART-IP Device](doc/3-Connecting%20to%20the%20device.r1.md)
- [4 Initial Device Provisioning](doc/4-Initial%20Device%20Provisioning.r1.md)
- [5 Working with the Device](doc/5-Working%20with%20the%20Device.r1.md)
- [6 Reading the Syslog](doc/6-Reading%20the%20syslog.r1.md)
- [Annex A About HART-IP Versions](doc/A-About%20HART-IP%20Versions.r1.md)
- [Annex B HART-IP Security and Factory Reset](doc/B-Security%20and%20Factory%20Reset.r1.md)
- [Annex C Building the Portable HART-IP Client](doc/C-Building%20the%20Portable%20HART-IP%20Client.md)


