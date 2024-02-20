# TOSR-RPi-network-manager
The Raspberry Pi network manager daemon for Tactical Open Source Radio - [TOSR](https://github.com/andrewmcdan/TOSR-main). 

### Goals
1. Establish a WiFi link between the RasPi's in each TOSR using a mesh topology
2. Have the capability to heal the mesh from the loss of connection between arbitrary nodes
3. Provide ethernet link via RJ45 connection to other devices.
4. Provide a virtual network interface that communicates over the digital VHF/UHF radio

### Considerations
- There will be 2 Wifi connections to manage (the RasPi's on-board Wifi and a USB connected Wifi adapter) and an ethernet connection, all three of which will need to be bridged.
- The on-board Wifi will be used in Station mode for connecting to other TOSR's. In the operation mode where an internet connection is to be established and shared amongst the mesh, one TOSR will be tethered to that internet connection to provide a mesh entry point for the other TOSR's.
- The secondary Wifi will operate in AP mode which other RasPi's / TOSR's will connect to. 
- Providing IP service via the VHF/UHF radio will require an entire IP stack and a virtual ethernet interface. It will be limited in throughput due to the nature of the radio's data link, and the fact that it will be sharing throughput with other data that the TOSR needs to send out. 
- The Wifi mesh manager, bridge manager, and VHF/UHF virtual ethernet services may have to be broken out into individual services due to the complexity of each, although they will have a need to communicate with each other for coordination. 
- The VHF/UHF IP network will be on a separate IP net than the ethernet / Wifi. Devices / services that are resilient to very low throughput networks will need to specifically route their traffic over this network. This will prevent having a device / service overload the very low throughput VHF/UHF IP network.

### Notes
- [RaspAP](https://raspap.com/) may be a worth exploring for control of the USB Wifi AP