# OCPP Ocular EVSE Home Assistant Integration

This repository is a personal Home Assistant custom integration fork for an
Ocular `OC20-BC-7kW-PLUS-V3` / Ocular 7kW Lite Plus charger using OCPP 1.6.

It is based on the upstream [`lbbrhzn/ocpp`](https://github.com/lbbrhzn/ocpp)
project, but this fork is now tuned for one practical use case:

- Home Assistant as the local OCPP central system.
- Ocular/Broadview single-phase 7kW charger.
- Manual installation into Home Assistant.
- Reliable maximum-current control through `number.charger_maximum_current`.
- Reconnect recovery that keeps charging stable through brief websocket drops.

This is not a HACS-supported integration and is not intended to be a
general-purpose OCPP distribution.

## Tested Charger

- Model: `OC20-BC-7kW-PLUS-V3`
- Common name: Ocular 7kW Lite Plus
- Home Assistant device name used during testing: `charger`
- Vendor reported by OCPP: `Broadview`
- Firmware seen during testing: `405.3251.0Q03196`
- OCPP protocol: `ocpp1.6`

## Current Working Behaviour

The Ocular charger has been tested with:

- Charging at 10A, 13A, and 32A from Home Assistant.
- Manual Home Assistant slider changes applying quickly to the charger.
- Home Assistant Core restart while plugged in and charging.
- Charger power-cycle while plugged in and charging.
- Brief websocket reconnects while charging.

The charger keeps charging at the last accepted current profile during short
OCPP disconnects, then resumes telemetry after reconnect.

## Recommended Control Method

Use:

```text
number.charger_maximum_current
```

Typical values:

```text
32A = full allowed charging
10A / 13A / 16A = limited charging
0A = requested pause, charger behaviour still needs careful validation
```

For this Ocular setup, avoid relying on `switch.charger_charge_control` for
scheduling. The most reliable path is the maximum-current number entity.

## Manual Installation

Copy only this folder into Home Assistant:

```text
custom_components/ocpp
```

The final path must be:

```text
/config/custom_components/ocpp/manifest.json
/config/custom_components/ocpp/__init__.py
```

Do not leave old copied folders in `/config/custom_components`, such as:

```text
ocpp - 0.10.20
ocpp v1
ocpp v2
```

Home Assistant scans every folder under `custom_components`, and bad folder
names can break loading.

After copying files, restart Home Assistant Core.

## Useful Logs

Reconnect and websocket behaviour:

```sh
ha core logs | grep -i "connection open\|reconnected\|Connection closed\|close frame\|protocol error\|invalid opcode\|opening handshake failed\|timed out\|ping=\|pong=\|Heartbeat\|BootNotification\|StatusNotification\|Current.Offered\|Current.Import" | tail -n 500
```

Charge-current control:

```sh
ha core logs | grep -i "Maximum Current\|Setting charge rate\|SetChargingProfile\|ClearChargingProfile\|Current.Offered\|Current.Import" | tail -n 160
```

Power-cycle recovery:

```sh
ha core logs | grep -i "BootNotification\|websocket\|connection open\|reconnected\|ChangeAvailability\|StatusNotification\|SetChargingProfile\|ClearChargingProfile\|Current.Offered\|Current.Import\|Heartbeat\|Connection closed" | tail -n 300
```

## Notes

This fork intentionally favours the behaviour that works with the tested Ocular
charger over broad charger compatibility. If you need a general OCPP Home
Assistant integration, use the upstream project instead.

## Upstream

Original project:

```text
https://github.com/lbbrhzn/ocpp
```
