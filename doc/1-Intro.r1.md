[PREVIOUS: Portable HART-IP Client ReadMe](../README.md)

# 1-Introduction 
The Portable HART-IP Client supports most current operating systems including Linux, MSWindows and MAC-OS. The Figure *Portable HART-IP Client Overview* shows its basic deployment.  The Portable HART-IP Client communicates with the HART-IP Server (e.g., the HART-IP Developer Kit).  

All HART devices have a real-time database that reflects the configuration of the device, current process conditions and the status of the device and connected process.  HART is the window through which the device interacts with the application.  The .NETCore backend of the Portable HART-IP Client maintains a subset of the devices database (using HART communication) and allows interaction with device itself.

<img src="../media/PHIP-Intro.r1.png" >

**Figure Portable HART-IP Client Overview**

A Web Browser is used to access and render the Portable HART-IP Client user interface.  The HTML5 VueClient frontend interacts with user, accesses the cached device data, and (indirectly) triggers further communication with the HART-IP server.

The Web Browser does not need to run on the same computer as the Portable HART-IP Client itself.  In fact, the Portable HART-IP Client (theoretically at least) could even be executing on the HART-IP Server.



A brief introduction to HART-IP, HART-IP Server, and HART-IP Clients are presented next.  This is followed by an introduction to the Portable HART-IP Client Architecture.

## HART-IP
HART-IP (Internet Protocol) serves as a high bandwidth PHY independent, connection between clients (data consumers) and servers (data producers).  It combines the ubiquitous Internet Protocol network infrastructure and the HART Protocol's network and application layers.  In other words, HART-IP is fundamentally the same HART Protocol many users are already using just running over IP networks.  As a result, plant personnel can utilize infrastructure already deployed and understood to provide HART compatible system connectivity, monitoring, control and device integration.

HART-IP communications is session oriented.  In other words, a HART-IP client opens a session with a server and the session remains open until the client closes the communications.  

### 	HART IP Servers
HART-IP servers monitor their IP connection and wait for a client to instantiate a session. Once the session is established, the HART-IP server must listen for HART-IP Client requests (e.g., a HART Command).  The request is processed and a response is returned to the client that made the request.  In addition to bidirectional request/response communication, servers must support unidirectional publishing of client-specified runtime process and status data.

Examples of servers include:

- Field Devices

- I/O Systems (Remote I/O and WirelessHART Gateways) and

- HART-IP Adapters.

In addition to native HART-IP servers, HART 4-20mA and WirelessHART devices can be accessed via the I/O Systems. So HART-IP can act as a high-speed backbone for communicating with already installed HART devices.

### HART-IP Clients
Clients are applications that interact with one or more field devices to perform its mission.  The Portable HART-IP Client itself is an example of a general purpose application that supports basic HART-IP operations.  Many other types of HART-IP Client applications are possible including:

- Control Systems and PLCs

- Data Historians

- Monitoring and Optimization Applications and

- Cloud-based data repositories.

## The Portable HART-IP Client

The Figure *Portable HART-IP Client Architecture* shows many internal details of the Portable HART-IP Client. This architecture aligns with many web-based applications world-wide.

- The HTML5 frontend presents a user interface using web pages to service each end user activity.  Commonly (like in banking applications) the frontend accesses  a database or data server that is used to populate the user interface. 

<img src="../media/PHIP-Architecture.r1.png" >

**Figure Portable HART-IP Client Architecture**

- A "REST-API" defines the interactions (methods and data) used to communicate  between the HTML5 frontend and the .NETCore backend.

- The .NETCore backend is the data and communication server for the Portable HART-IP Client. Using .NETCore enables the Portable HART-IP Client to be platform independent.


### HTML5 Frontend
The Portable HART-IP Client is based on HTML5 using the "Reactive Design" technique.  Each of the screens / tabs consist of a combination of HTML, CSS (style sheets), JS (Sava Script). 

- The HTML CSS define visualization of the pages.
- JS updates pages while communicating with backend via Rest API

Basically there is one {HTML, CSS, JS} per page.  To simplify and accelerate development the [Vue](https://vuejs.org) framework / development environment is used.    

 
### .NETCore backend
The portable .NETCore back end is the  Data/Information engine for Portable HART-IP Client User interface.  Is uses the REST API to interact with the user Interface and a HART-IP Client to interact with the device itself.

To support communication with the device it includes a Command Dispatcher the sends and receives communication plus a Parser to consume the HART binary data.  Fundamentally this helps ensure the locally cached data matches that in the HART-IP device's real-time database.  It also support on demand / adhoc communication triggered by the Portable HART-IP Client's operator/user.

Enabling the backend is [HART DeviceInfo](https://www.fieldcommgroup.org/integration-technologies/deviceinfo).  DeviceInfo are JSON files that provide a simple mode of a HART field device.  The Portable HART-IP Client has a core set of HART Command and Data modeled using the DeviceInfo conventions.  Not only are the data modeled, metadata (like labels, unit code strings, the meanings of status bits) are included as well.  

The [FDI tools](https://www.fieldcommgroup.org/technologies/fdi/fdi-development-tools#4257225834-2762024773) can also emit a DeviceInfo files for a specific field device.  This device-specific DeviceInfo file can be imported.  This allows, for example, all of the strings for device's Command 48 Status bits to be presented in the Portable HART-IP Client User Interface. The DeviceInfo file can be found in the device's FDI Device Package.

The backend also includes Controllers that service requests/ inquiries from Rest API. Essentially the JS on the frontend accesses the REST API as needed by the User and the controllers on the backend fulfill those needs and trigger communications with the device when needed.


[NEXT: Overview of Portable HART-IP Client Operation](./2-Overview.r1.md)
