[PREVIOUS: Reading the Syslog](./6-Reading%20the%20syslog.r1.md)

# A-HART-IP Fundamentals: About HART-IP Versions
There are two versions of HART-IP.  The Portable HART-IP Client supports both versions.  This chapter provides an overview of the two versions and guidance on configuring the version of HART-IP for the Portable HART-IP Client's use

- **v1**. v1 was first fielded in 2009 and evolved from application notes to full specification status by 2012.  Historically v1 has been used for Remote I/O and WirelessHART Gateways. Security is mandatory but the responsibility of the manufacturer.

- **v2**. Released in 2020, v2 is a major improvement.  V2 has mandatory minimum security suites, Audit Logs, syslogging and more.  It includes many clarifications and incorporates lessons-learned over the last 10 years.

Fundamentally both are HART - They use the same Application Layer, work with the same tools as other HART devices and are backward compatible with each other.  Because of the coupling between backward compatibility and security there are some subtle nuances that should be considered when configuring the Portable HART-IP Client.

## Backward Compatibility
With the release of v2 HART backward compatibility rules were carefully required.  At the same time, robust cybersecurity was essential and will not be compromised.  The following Table summarizes the possible client/server modes of operation.  Conceptually - 

- HART-IP clients must adapt to the HART-IP Version returned by the server (e.g., field device).

- Servers reply to v1 client session initiate as a v1 Server.  v1 clients (which have been around >10 years) may not be compliant and operate in forward compatibility and HART-IP v2 does not abandon them

- When both client and server are v2 then standardized security must be utilized.

**Table HART-IP Backward Compatible Operation**


|**Server** >|1|2|
|:--|:--|:--|
|**Client**  v| | |
|**1** | Normal Operation. | Server runs in v1 backward compatible mode. |
|**2** | Client falls back to v1.  | Normal Operation.  Standardized secure communication  |

## Choosing the Server's Version
Immediately after a [Factory Reset](B-Security%20and%20Factory%20Reset.r1.md) v2 HART-IP Servers can be initialized to operate as either as a v1 or a v2 HART-IP device.  Not both.  Once the Server is initialized it will stay in the version selected until a [Factory Reset](B-Security%20and%20Factory%20Reset.r1.md) is performed.  

Choosing whether to initialize the Server to v1 or v2 can be decided based on a few questions

|Q. | A.|
|:--|:--|
|Will a HART-IP v1 Client ever be used with the Server? | If so, choose v1|
|Will existing Servers be updated to v2| If so, choose v2|
|Security is essential to your installation | If so, choose v2|

Clearly, leveraging HART-IP v2 security is the best, most robust choice in most cases.  That being said, backward compatible HART-IP v1 is available. Ultimately the end user can choose to deploy HART-IP devices as the best interoperate with their existing installations. 


## Choosing Client's HART-IP Version
HART-IP v2 Clients must operate in backward compatible mode to seamlessly work with HART-IP v1 devices.  So, in most cases, the Client Version should be set to 2.

There is one exception to this rule: when using the Portable HART-IP Client to initialize a Server into HART-IP v1.  In this case, the Client Version must be set to 1 and (immediately after [Factory Reset](B-Security%20and%20Factory%20Reset.r1.md)) used to provision the Server.  Since the first connection is to a HART-IP v1 Client the Server will set itself to v1 and stay that way permanently (i.e., until another [Factory Reset](B-Security%20and%20Factory%20Reset.r1.md)).

[NEXT: Annex B HART-IP Security and Factory Reset](./B-Security%20and%20Factory%20Reset.r1.md)
