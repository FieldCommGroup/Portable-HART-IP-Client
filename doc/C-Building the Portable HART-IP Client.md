[PREVIOUS: Annex B HART-IP Security and Factory Reset](./B-Security%20and%20Factory%20Reset.r1.md)

# C-Building the Portable HART-IP Client

These instructions describe how to build, deploy and use the client.

## Prerequisites

1. A HART-IP device or server that supports the HART-IP v1 or v2.
2. Visual Studio 2022 or later.
For Visual Studio 2022, make sure ".NET Core cross platform development" is selected in the toolset during installation. Otherwise you can modify this from the Visual Studio installer after installation.
3. .NET 6 SDK


## Build and Test
1. Clone the repository from [here](https://github.com/FieldCommGroup/NetCoreHartIpClient/).

2. If publishing to Linux or MAC install openssl on those platforms. Windows OpenSSL library has already been included.

3. Open the solution **HartIPdotNET.sln** in Visual Studio 2022

4. Build the Vue Client project as described below.

5. Build and run the HartIPdotNET project.

6. Start your browser at http://localhost:5005/#/

7. Connect to hipserver/device by selecting 'Connect' and entering IP address, Port, UDP or TCP connection and SRP or PSK encryption.

## Vue Client
Install PowerShell command line (Windows/Mac/Linux/ARM) from [here](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell)

1. Traverse to \HartIPdotNET\VueClient using PowerShell Command Line.
2. If you have never installed yarn on your machine before, install Node.js first from [here](https://nodejs.org/en/)

3. After installing nodejs, install yarn via npm:
 ```text
npm install --global yarn
```
4. Run the following from the "VueClient" folder using Windows PowerShell.
 ```text
yarn install
yarn build
```



Alternatively, if you want to run the client separately when making changes to the VueClient and don't want to rebuild the server, you still could run this under VS code on the VueClient folder:
 ```
yarn serve
```
Access the page using a browser at address http://localhost:5005

## Using Docker

You can use the client simply without rebuilding it each time by installing it into a Docker container. 

Download and install Docker from [here](https://www.docker.com/get-started).


From the project's root folder, (docker-compose.yml is located in this folder), build a new container by running from the command line:
```
docker-compose build
```

Start the container:
```
docker-compose up
```

navigate to http://localhost:5005 to see the HART-IP Client's user interface in your browser .

Stop the container:
```
docker-compose down
```


## Other run options
When _rebuildClient set to true on Startup.cs, when running the DotNetCore server, 'yarn serve' would be executed automatically, and Vue client changes would reflect instantly in the browser.

If you want to run the DotNetCore server without rebuilding the Vue client, set this in the Startup.cs constructor:
 ```
_rebuildClient = false;
```

The false flag would allow you to load up the prebuilt Vue client.
 ```
_rebuildClient = true;
```

# Debugging from Visual Studio 2022
1. Open HartIPdotNET.sln
2. Make sure HartIPdotNET is selected instead of IIS Express in the ► Debugging configuration unless you intend to use IIS
3. Start Debugging

# Installing .NET 6 SDK for Windows
Download and install from here:
https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/sdk-6.0.101-windows-x64-installer

# Installing .NET 6 SDK for Linux
First, add the Microsoft package repository to your system's package list. In addition, include Microsoft's package signing key to your collection of trusted keys. Example is for Ubuntu.

`wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb`
`sudo dpkg -i packages-microsoft-prod.deb`

After adding the new package repository, get the latest package information from your package sources using apt.

`sudo apt update`

To be able to install the .NET SDK securely via HTTPS, make sure to install the apt-transport-https package using the command below.

`sudo apt install apt-transport-https`

Then, install the .NET 6 SDK using the following command.

`sudo apt-get install -y dotnet-sdk-6.0`

To check if .NET 6 has been installed successfully, you can run the following command to list available SDKs on your system. If you have multiple SDKs installed, they will all be listed here.

`dotnet --list-sdks`

# Building HartIPdotNET for Windows
Run the following command on the root directory
`dotnet publish -c PublishRelease`

Navigate to HartIPdotNET/bin/PublishRelease/net6.0/publish and run the following to test:
`HartIPdotNET.exe`

# Building HartIPdotNET for Linux
Run the following command on the root directory
`dotnet publish -c PublishRelease`

Navigate to HartIPdotNET/bin/PublishRelease/net6.0/publish and run the following to test:
`./HartIPdotNET`

# Credential Storage - Security Manager
If you want to have your credentials to different HART-IP servers saved and persisted, please start the KeyService before running the .NET 6 Service. No edits would need to be made to the client. However, if you want to change the port and address of the KeyService API, change the following line in appsettings.json inside the HARTIPdotNET folder:

`"LocalKeyVaultUrl": "https://localhost:5001/"`

The KeyService repo located here: https://github.com/FieldCommGroup/HartIpSecurityManager/

Instructions on how to build and start the KeyService is written on the repo's README.md.
 
[UP: Portable HART-IP Client ReadMe](../README.md)
