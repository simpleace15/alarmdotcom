<h4 align="center">⚠️ Community-maintained fork — the upstream project
(<a href="https://github.com/pyalarmdotcom/alarmdotcom">pyalarmdotcom/alarmdotcom</a>) has paused maintenance.
This fork carries HA 2026.x compatibility fixes. See <a href="#about-this-fork">About this fork</a>.</h4>

<p align="center"><img src="https://user-images.githubusercontent.com/466460/175781161-dd70c5b4-d45a-4cdb-bf57-d4fd7fbedb0b.png" width="125"></a>
<h1 align="center">Alarm.com for Home Assistant</h1>
<p align="center">This is an unofficial project that is not affiliated with Alarm.com</p>
<br />

<hr />

This is a custom component that allows Home Assistant to interface with [Alarm.com](https://www.alarm.com/) by using the Alarm.com website's unofficial API. This component is designed primarily to integrate the Alarm.com security system functions; as such, it requires an Alarm.com package which includes security system support.

Please note that Alarm.com may break functionality at any time.

![image](https://user-images.githubusercontent.com/466460/171702200-c5edd68b-c54f-4ca4-82b3-d5a0bb97702b.png)

![image](https://user-images.githubusercontent.com/466460/171701963-e5b5f765-6817-4313-8fa1-6035f4c453e9.png)

## Safety Warnings

This integration is great for casual use within Home Assistant but... **do not rely on this integration to keep you safe.**

1. This integration communicates with Alarm.com over an unofficial channel that can be broken or shut down at any time.
2. It may take several minutes for this integration to receive a status update from Alarm.com's servers.
3. Your automations may be buggy.
4. This code may be buggy. It's written by volunteers in their free time and testing is spotty.

You should use Alarm.com's official apps, devices, and services for notifications of all kinds related to safety, break-ins, property damage (e.g.: freeze sensors), etc.

Where possible, use local control for smart home devices that are natively supported by Home Assistant (lights, garage door openers, etc.). Locally controlled devices will continue to work during internet outages whereas this integraiton will not.

## Details

### Supported Devices

| Device Type       | Actions                               | View Status | Low Battery Sub-Sensor | Malfunction Sub-Sensor | Configuration Options                                                                | Notes                                                                                                                                                                                                          |
| ----------------- | ------------------------------------- | ----------- | ---------------------- | ---------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Alarm System      | arm away, arm stay, arm night, disarm | ✔          | ✔                     | ✔                     |                                                                                      |                                                                                                                                                                                                                |
| Garage Door       | open, close                           | ✔          | ✔                     | ✔                     |                                                                                      |                                                                                                                                                                                                                |
| Gate              | open, close                           | ✔          | ✔                     | ✔                     |                                                                                      |                                                                                                                                                                                                                |
| Light             | turn on / set brightness, turn off    | ✔          | ✔                     | ✔                     |                                                                                      |                                                                                                                                                                                                                |
| Lock              | lock, unlock                          | ✔          | ✔                     | ✔                     |                                                                                      |                                                                                                                                                                                                                |
| Sensor            | _(none)_                              | ✔          | ✔                     | ✔                     |                                                                                      | Contact sensors will not report the same state within a 3-minute window. This means that Home Assistant will only be notified once if, say, a door has been opened and closed multiple times within 3 minutes. |
| Skybell HD Camera | _(none)_                              |             | ✔                     | ✔                     | Indoor Chime On/Off, Outdoor Chime Volume, LED Brightness, Motion Sensor Sensitivity | No video support!                                                                                                                                                                                              |
| Thermostat        | heat, cool, auto heat/cool, fan only  | ✔          | ✔                     | ✔                     |                                                                                      | Fan only mode turns on the fan for the maximum duration available through Alarm.com. There is no option to turn on the fan for a shorter duration. Also, no support for remote temperature sensors.            |

### Supported Sensor Types

| Sensor Type             | Notes                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Contact                 | Doors, windows, etc.                                                                                                                                                                        |
| Freeze                  |                                                                                                                                                                                             |
| Glass Break / Vibration | Both standalone listeners (e.g.: [DSC PGx922](https://www.dsc.com/?n=products&o=view&id=2585)) & control-panel built-ins (e.g. [Qolsys IQ Panel 4](https://qolsys.com/panel-glass-break/)). |
| Motion                  |                                                                                                                                                                                             |
| Vibration Contact       | Doors, windows, safes, etc. (e.g.: [Honeywell 11](https://www.alarmgrid.com/products/honeywell-11))                                                                                         |
| Water                   |                                                                                                                                                                                             |

Note that Alarm.com can has multiple designations for each sensor and not all are known to the developers of this integration. If you have one of the above listed devices but don't see it in Home Assistant, [open an issue on GitHub](../../issues/new/choose).

#### Subsensors

Each sensor in your system is created as both a device and as an entity within Home Assistant. Each device has an associated low battery sensor that activates when the device's battery is low. Each device also has an associated malfunction sensor that activates when either Alarm.com reports an issue or when this integration is unable to process data for a sensor.

### Future Support

#### Roadmapped Devices

The developers have access to the devices listed below and plan to add support in a future release.

| Device Type  | Notes                                                                                                                                                 |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Image Sensor | _Not_ video cameras. Image sensors (e.g.: [Qolsys Image Sensor](https://qolsys.com/image-sensor/)) take still photos when triggered by motion events. |

#### Help Wanted Devices

If you own one of the below devices and want to help build support, [open an issue on GitHub](../../issues/new/choose).

| Device Type        | Notes                                                                                                                    | Help Needed |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------ | ----------- |
| RGB Light          | e.g.: [Inovelli RGBW Smart Bulb](https://inovelli.com/rgbw-smart-bulb-z-wave/)                                           | A lot.      |
| Temperature Sensor | e.g.: [Alarm.com PowerG Wireless Temperature Sensor](https://suretyhome.com/product/powerg-wireless-temperature-sensor/) | A little.   |
| Video Camera       | e.g.: [Alarm.com ADC-V515](https://www.alarmgrid.com/products/alarm-com-adc-v515)                                        | A lot.      |
| Water Valve        | e.g.: [Dome Water Main Shut-off](https://www.domeha.com/z-wave-water-main-shut-off-valve)                                | A lot.      |

##### Help Needed Scale

-   **A lot:** You'll need to know how to capture web traffic. We'll ask you to log into Alarm.com and use your web browser's network inspector tool to capture requests for all of your device's functions.
-   **A little:** We'll ask you to run a Python script to dump metadata for your devices. This is straightforward and doesn't require much technical skill.

#### Device Blacklist

These devices are known but blocked from appearing in Home Assistant. If you disagree with any of these ing reasons, please [open an issue on GitHub](../../issues/new/choose)!

| Device Type        | Reason                                                                                                                                                                                                                                                                                                           |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Audio Systems      | Alarm.com supports Sonos systems, but Home Assistant has a better, built-in integration for these devices.                                                                                                                                                                                                       |
| Blinds and Shades  | _(See above.)_                                                                                                                                                                                                                                                                                                   |
| Carbon Monoxide    | Doesn't support state reporting. May be supported in the future.                                                                                                                                                                                                                                                 |
| Irrigation Systems | Like above, Home Assistant probably has better direct integrations for these devices.                                                                                                                                                                                                                            |
| Mobile Phones      | Some control panels support PIN-less proximity unlocking via bluetooth (e.g.: [Qolsys IQ Panel 4](https://qolsys.com/bluetooth/)). Paired mobile phones appear in Alarm.com as sensors, but don't provide any useful functions or information for use in Home Assistant (not even malfunction or battery level). |
| Panic              | Doesn't support state reporting. May be supported in the future.                                                                                                                                                                                                                                                 |
| Smoke              | Doesn't support state reporting. May be supported in the future.                                                                                                                                                                                                                                                 |


## About This Fork

The upstream project ([pyalarmdotcom/alarmdotcom](https://github.com/pyalarmdotcom/alarmdotcom)) paused
maintenance in August 2026 after its maintainer lost access to an Alarm.com system. Home Assistant's
2025.12–2026.x releases broke this integration in several ways. This fork is the actively maintained
line and is based on the [Bonasort-HA](https://github.com/Bonasort-HA/alarmdotcom) fork (v3.0.14.5),
with the following fixes on top (v3.0.16.0):

- **HA 2026 compat** (from Bonasort v3.0.14.1–.5): entities no longer crash with
  `AttributeError: '_friendly_name_internal'`, panel states use the supported
  `AlarmControlPanelState` API, options-flow + config-entry migration fixes, thermostat
  color-mode/feature migration, websocket push no longer tears down on unknown devices.
- **Reauth/reconfigure crash fixed** (port of upstream PR #546): reauth on HA 2025.12+ no longer
  fails with "Unknown error".
- **From upstream v3.0.15**: correct panel states on HA 2025.11+.
- **From nulledy v3.0.15.2**: arming/disarming from Home Assistant without a panel code is allowed.
- **`beautifulsoup4` pinned >= 4.13.4**: fixes `No module named 'bs4._typing'` startup crash on
  HA 2026.8+ (a stale/partial bs4 install made the loose `>=4.10.0` pin unfixable by HA).
- Integration now installs this fork's own copy of the `pyalarmdotcomajax` library
  (the linked fork of [pyalarmdotcom/pyalarmdotcomajax](https://github.com/pyalarmdotcom/pyalarmdotcomajax)
  in this account) pinned at v0.5.13.2, so library changes can't silently break the integration.

Supported/reported working on: Home Assistant **2026.9** (works back through ~2026.2, forward to 2026.10
expected). If you're switching from the v4.0.1-beta line, re-configure the integration (settings may
not carry over).

## Using the Integration

### Installation

1. Use [HACS](https://hacs.xyz/) to download this integration.
2. Configure the integration via Home Assistant's Integrations page. (Configuration -> Add Integration -> Alarm.com)
3. When prompted, enter your Alarm.com username, password, and two-factor authentication one-time password.

### Configuration

You'll be prompted to enter these parameters when configuring the integration.

| Parameter         | Required | Description                                                   |
| ----------------- | -------- | ------------------------------------------------------------- |
| Username          | Yes      | Username for your Alarm.com account.                          |
| Password          | Yes      | Password for your Alarm.com account.                          |
| One-Time Password | Maybe    | Required for accounts with two-factor authentication enabled. |

#### Additional Options

These options can be set using the "Configure" button on the Alarm.com card on Home Assistant's Integrations page:

![image](https://user-images.githubusercontent.com/466460/150607393-e057d445-a882-4fbd-a455-acf155083327.png)

| Parameter       | Description                                                                                                                                                                                                                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Code            | Specifies a code to arm/disarm your alarm or lock/unlock your locks in the Home Assistant frontend. This is not necessarily the code you use to arm/disarm your panel. This is a separate code that Home Assistant in [alarm panel card](https://www.home-assistant.io/dashboards/alarm-panel/). |
| Force Bypass    | Bypass open zones (windows, doors, etc.) when arming.                                                                                                                                                                                                                                            |
| No Entry Delay  | Bypass the entry delay normally applied to entrance sensors.                                                                                                                                                                                                                                     |
| Silent Arming   | Suppress beeps when arming and double arming delay length.                                                                                                                                                                                                                                       |
| Update Interval | Frequency with which this integration should poll Alarm.com servers for updated status.                                                                                                                                                                                                          |

_The three arming options are not available on all systems/providers. Also, some combinations of these options are incompatible. If arming does not work with a combination of options, please check that you are able to arm via the web portal using those same options._
