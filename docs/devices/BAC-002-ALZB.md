---
title: "Tuya BAC-002-ALZB control via MQTT"
description: "Integrate your Tuya BAC-002-ALZB via Zigbee2MQTT with whatever smart home infrastructure you are using without the vendor's bridge or gateway."
addedAt: 2021-03-28T13:25:07Z
pageClass: device-page
---

<!-- !!!! -->
<!-- ATTENTION: This file is auto-generated through docgen! -->
<!-- You can only edit the "Notes"-Section between the two comment lines "Notes BEGIN" and "Notes END". -->
<!-- Do not use h1 or h2 heading within "## Notes"-Section. -->
<!-- !!!! -->

# Tuya BAC-002-ALZB

|     |     |
|-----|-----|
| Model | BAC-002-ALZB  |
| Vendor  | [Tuya](/supported-devices/#v=Tuya)  |
| Description | FCU thermostat temperature controller |
| Exposes | climate (local_temperature, system_mode, fan_mode, current_heating_setpoint, preset, local_temperature_calibration), child_lock, schedule, max_temperature, deadzone_temperature |
| Picture | ![Tuya BAC-002-ALZB](https://www.zigbee2mqtt.io/images/devices/BAC-002-ALZB.png) |


<!-- Notes BEGIN: You can edit here. Add "## Notes" headline if not already present. -->
## Notes


### Pairing
Switch the thermostat off. Press and hold the temperature down button for +- 8 seconds to enable the pairing mode (display lights up and a WiFi-like icon is blinking). After successful interview turn the thermostat on again.

### Stop message flooding
This unit has a bug that makes it send multiple messages when updating. To stop this from flooding your MQTT Queues, please add the following to your `configuration.yaml` file:


devices:
  '0x12345678':
    friendly_name: thermostat
    debounce: 1
<!-- Notes END: Do not edit below this line -->



## Options
*[How to use device type specific configuration](../guide/configuration/devices-groups.md#specific-device-options)*

* `control_sequence_of_operation`: Operating environment of the thermostat. The value must be one of `cooling_only`, `cooling_and_heating_4-pipes`


## Exposes

### Climate 
This climate device supports the following features: `local_temperature`, `system_mode`, `fan_mode`, `current_heating_setpoint`, `preset`, `local_temperature_calibration`.
- `current_heating_setpoint`: Temperature setpoint. To control publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"current_heating_setpoint": VALUE}` where `VALUE` is the °C between `5` and `35`. Reading (`/get`) this attribute is not possible.
- `local_temperature`: Current temperature measured on the device (in °C). Reading (`/get`) this attribute is not possible.
- `system_mode`: Mode of this device. To control publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"system_mode": VALUE}` where `VALUE` is one of: `off`, `cool`, `heat`, `fan_only`. Reading (`/get`) this attribute is not possible.
- `preset`: Mode of this device (similar to system_mode). To control publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"preset": VALUE}` where `VALUE` is one of: `auto`, `manual`. Reading (`/get`) this attribute is not possible.
- `local_temperature_calibration`: Offset to add/subtract to the local temperature. To control publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"local_temperature_calibration": VALUE}.`The minimal value is `-3` and the maximum value is `3` with a step size of `1`.

### Child lock (binary)
Enables/disables physical input on the device.
Value can be found in the published state on the `child_lock` property.
It's not possible to read (`/get`) this value.
To write (`/set`) a value publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"child_lock": NEW_VALUE}`.
If value equals `LOCK` child lock is ON, if `UNLOCK` OFF.

### Schedule (composite)
Auto-mode schedule, 4 periods each per category. Example: "06:00/20 11:30/21 13:30/22 17:30/23.5"..
Can be set by publishing to `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"schedule": {"weekdays": VALUE, "saturday": VALUE, "sunday": VALUE}}`
- `weekdays` (text): Schedule (1-5), 4 periods in format "hh:mm/tt". 
- `saturday` (text): Schedule (6), 4 periods in format "hh:mm/tt". 
- `sunday` (text): Schedule (7), 4 periods in format "hh:mm/tt". 

### Max temperature (numeric)
Maximum temperature.
Value can be found in the published state on the `max_temperature` property.
It's not possible to read (`/get`) this value.
To write (`/set`) a value publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"max_temperature": NEW_VALUE}`.
The minimal value is `35` and the maximum value is `45`.
The unit of this value is `°C`.
Besides the numeric values the following values are accepted: `default`.

### Deadzone temperature (numeric)
The delta between local_temperature and current_heating_setpoint to trigger activity.
Value can be found in the published state on the `deadzone_temperature` property.
It's not possible to read (`/get`) this value.
To write (`/set`) a value publish a message to topic `zigbee2mqtt/FRIENDLY_NAME/set` with payload `{"deadzone_temperature": NEW_VALUE}`.
The minimal value is `1` and the maximum value is `5`.
The unit of this value is `°C`.
Besides the numeric values the following values are accepted: `default`.

