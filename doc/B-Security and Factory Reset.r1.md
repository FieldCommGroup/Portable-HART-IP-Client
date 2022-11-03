[PREVIOUS: Annex A About HART-IP Versions](./A-About%20HART-IP%20Versions.r1.md)

# B-HART-IP Fundamentals: About Security and Factory Reset

The initial deployment of a HART-IP device is pivotal and configures the device for the network it will be attached to and configures the initial security credentials for forthcoming client connections.  

## Factory Reset
Central to ensuring HART-IP's security is Factory Reset. Factory Reset requires physical access to the device and is performed while cycling power to the device.  Factory Reset is enabled manually using (for example) a jumper or push-button.

Factory Reset results in 

- Known security credentials
- Known HOSTNAME (the hyphenated MAC address)
- A one time initial session

The default security credentials are used in the initial connection.  This allows the new security credentials to be provisioned using secure communications.  After the initial session all security credentials are secret.

## What happens after Factory Reset
After a Factory Reset all parameters in the device are reset to their factory settings.  This includes 

- Range Values
- Unit codes
- Dynamic Variable mapping (if supported)
- Burst messages
- Alarm levels (if supported) 
- HOSTNAME (device's MAC Address)
- Supplemental IP Ports are set to the default value of 5094
- Defaulting the Slot 0 ("Security Manager") credentials

This means physical access to the device is required and after performing Factory Reset the device configuration is erased.  Because of the pain and disruption Factory Reset is noticeable and not undertaken trivially.  


## HART-IP Security
HART-IP v1 requires security but choice of security delegated to the manufacturer.  HART-IP v2 includes mandatory security and specifies minimum set of IP TLS Cypher Suites.  To ensure robust security HART-IP requires the server to be locked into either v1 or v2 mode.  This "locking" occurs upon the initial communication session after Factory Reset"  

Just after Factory Reset, the server locks to the HART Version (v1 or v2) supported by the first client connecting to the device.  In other words:

- If initial connection is made by a v1 client then the server will subsequently only connect to a v1 client.  Native security is disabled.

- If initial connection is performed by a v2 client then security credentials must be provisioned during that initial connection.  Subsequently the server will only connect (securely) to a v2 client.

Basically the end user can engineer/design the installation to use security or not based on the currently deployed applications and HART-IP devices (e.g., Remote I/O).  Secure and in-secure communications to the server cannot be mixed simultaneously on the same device.  It is one or the other (v1 unsecure or v2 secure).  The end user controls and makes that choice.

[NEXT: Annex C Building the Portable HART-IP Client](./C-Building%20the%20Portable%20HART-IP%20Client.md)
