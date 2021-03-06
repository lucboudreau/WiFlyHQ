A library for the Roving Networks WiFly RN-XV.

The library provides functions for setting up and managing the WiFly module,
sending UDP packets, opening TCP connections and sending and receiving data
over the TCP connection.

Example code to setup and use the hardware serial interface:

	Serial.begin(9600);
	wifly.begin(&Serial, NULL);

Setup and use a software serial interface:

	#include <SoftwareSerial.h>
	SoftwareSerial wifiSerial(8,9);

	wifiSerial.begin(9600);
	wifly.begin(&wifiSerial);

Join a WiFi network:

	wifly.setSSID("mySSID");
	wifly.setPassphrase("myWPApassword");
	wifly.enableDHCP();
	wifly.join();

Send a UDP packet:

	wifly.setIpProtocol(WIFLY_PROTOCOL_UDP);
	wifly.sendto("Hello, world", "192.168.1.100", 2042);

Open a TCP connection and send some data, and close the connection:

	wifly.setIpProtocol(WIFLY_PROTOCOL_TCP);
	wifly.open("192.168.1.100",8042);
	wifly.println("Hello, world!");
	wifly.close();

Receive UDP or TCP data (assumes software serial interface):

	if (wifly.available() > 0) {
	    Serial.write(wifly.read());
	}

Limitations with WiFly RN-XV rev 2.32 firmware
1. Cannot determine the IP address of the TCP client that has connected.
2. Changing the local port does not take effect until after a save and reboot.
3. Closing a TCP connection may not work. Client may stay connected
   and send additional data.

To do:
1. Add support for adhoc mode.
