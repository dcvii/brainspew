---
title: "Understanding Device LED Status Indicators"
source: "https://help.ui.com/hc/en-us/articles/204910134-Understanding-Device-LED-Status-Indicators"
author:
published:
created: 2026-07-25
description: "Learn how to identify your device's state based on the LED color patterns. These blue and white status LEDs apply to all our UniFi access..."
tags:
  - "brain_spew"
---
Learn how to identify your device's state based on the LED color patterns. These **blue and white status LEDs** apply to all our UniFi access points, routers, switches, and the UDM base model.

## Status LED Patterns

***Note:** The animations are for illustrative purposes - the speed of the flashing or strobing patterns below might differ slightly from your device's.*

The device is initializing and booting up.

![UAP-AC-1-Initializing.gif](https://help.ui.com/hc/article_attachments/203198938)

The device is ready for [adoption](https://help.ui.com/hc/en-us/articles/360012622613).

![UAP-AC-2-Factory-Defaults.gif](https://help.ui.com/hc/article_attachments/203134967)

A client device is connected to the UDM via Bluetooth.

![UDM-BLE.gif](https://help.ui.com/hc/article_attachments/360058275714)

There is no internet connection to the UDM.

![UDM-NO_WAN.gif](https://help.ui.com/hc/article_attachments/8423839885975)

### Steady Blue

The device is adopted and is in normal operating mode. Access Point is broadcasting WiFi.

![UAP-AC-4-Adopted.gif](https://help.ui.com/hc/article_attachments/203198958)

### Strobing White / Off

If this happens, power cycle the Access Point.

If this doesn't help, please [reach out to our support team](https://help.ui.com/hc/en-us/requests/new).

![UAP-AC-9-Error-A12.gif](https://help.ui.com/hc/article_attachments/360100808973)

### Quickly Flashing White / Blue

The device firmware is currently being upgraded - do not interrupt the process.

UDM will flash only white during an upgrade.

![UAP-AC-7-Firmware-Upgrade.gif](https://help.ui.com/hc/article_attachments/203134977)

### Blue and Flashing Off Every 5s

Access Point has lost network connectivity and is searching for a wireless uplink.

![UAP-AC-5-Isolated.gif](https://help.ui.com/hc/article_attachments/203202488)

### Rapid Flashing Blue / Off

The device "Locate" feature was activated in the UniFi Network application.

![UAP-AC-6-Locating.gif](https://help.ui.com/hc/article_attachments/203202498)

### Flashing White-Blue-Off

The device is in TFTP mode.

To enable this mode:

1. Hold the reset button before powering on.
2. Continue to hold the reset button until this LED sequence appears.

If this wasn't intentional, please ensure the device's reset button isn't jammed (it should click when pushed).

![UAP-AC-TFTP.gif](https://help.ui.com/hc/article_attachments/115024215128)

### LED Off

The device is offline.

Verify the Power, POE, and Ethernet cables to troubleshoot.

![UAP-AC-8-LED-Off.gif](https://help.ui.com/hc/article_attachments/203144387)

## UniFi Bridge to Bridge (UBB)

Including the statuses described above, the UBB has two additional ones:

### Red with Circulating Blue LED

The 60 GHz link cannot be established or has dropped due to bad weather. If the UBB fails over to 5 GHz, the LED will remain red. When the 60 GHz link is re-established, the LED will turn blue (or the custom color selected in the UniFi Network application).

***Note:** If the other bridge device is within range and the UBB LED is red, we recommend adjusting the UBB's position to enhance the signal strength.*

### Green

If the Alignment Tool enabled in the UniFi Network application, a green LED means the UBB devices are properly aligned.

***Note:** If the other bridge device is within range and the UBB LED is green and red, we recommend adjusting the UBB's position until the LED is green.*

## UniFi Mobile Routers (UMR-Industrial & UMR-Ultra)

Including the statuses described above, the UMR-Industrial & UMR-Ultra have two additional ones:

**Blinking Blue Every 3.2 Seconds (3 seconds Blue, 0.2 seconds off)**

Network Error / WiFi Error (Device on but no connect to the Internet)

**Blinking White Every 3.2 Seconds (3 seconds White, 0.2 seconds off)**

SIM card initialization unsuccessful (SIM card locked or deactivated)

***Note:** To unlock the SIM or configure the correct APN settings, use a web browser to go to the local portal (192.168.105.1). Log in with the default admin password ("ui").*

For UMR LED indicators please refer [here](https://help.ui.com/hc/en-us/articles/31169556838807-Getting-Started-with-UniFi-Mobile-Router-Series).

## LED Patterns for Ports

UniFi Security Gateways and UniFi Switches vary in port types, numbers, and locations. For detailed information on the ports for your specific device model, consult its Quick Start Guide.

**Console Port's right LED (in the applicable devices):**

- LED Off: Power Off
- LED Green: Power On

**Speed/Link/Act (right LED ports other than Console):**

- LED Off: No Link
- LED Amber: Link Established at 10/100 Mbps
- LED Flashing Amber: Link Activity at 10/100 Mbps
- LED Green: Link Established at 1000 Mbps
- LED Flashing Green: Link Activity at 1000 Mbps

**PoE (left LED on ports of applicable devices):**

- LED Off: No PoE
- LED Amber: IEEE 802.3af/802.3at
- LED Green: 24V Passive

**SFP (in the applicable devices):**

- LED Off: No Link
- LED Green: Link Established at 1 Gbps
- LED Flashing Green: Link activity at 1 Gbps

See specific port LED information in the Hardware Overview section (between pages 5 and 6) of the Quick Start Guides (QSG). You can find the QSGs in the Documentation section of our [UniFi Downloads](https://www.ui.com/download/unifi/) page, by searching for the device in question in the left-hand menu.

## LED Patterns for PoE Adapters

**LED is Off:** PoE is Off.

**LED is On and Steady**: PoE is functioning as it should.

**LED is Blinking:** this is not a configured state, this may indicate that the device is not connected properly, or that something is wrong with the cable.

## How to Disable Device LEDs

1. Go to *UniFi* *Devices* and click on the device you wish to edit to bring up its **Properties** panel
2. Go to *Settings* and adjust the LED settings.