# Installation

This fork is installed manually. Do not install it through HACS.

## Copy Files

Copy the repository folder:

```text
custom_components/ocpp
```

to Home Assistant:

```text
/config/custom_components/ocpp
```

The target folder should contain files such as:

```text
/config/custom_components/ocpp/manifest.json
/config/custom_components/ocpp/__init__.py
/config/custom_components/ocpp/chargepoint.py
```

Remove old test copies from `/config/custom_components`, for example:

```text
ocpp - 0.10.20
ocpp v1
ocpp v2
```

Home Assistant tries to load every folder under `custom_components`, so old
copies can cause confusing import errors.

## Restart Home Assistant

Restart Home Assistant Core after copying the files.

## Configure OCPP

The tested setup uses:

```text
Host: 0.0.0.0
Port: 9000
Charge point identity: central
Protocol: ocpp1.6
```

The charger should point at the Home Assistant OCPP websocket, for example:

```text
ws://homeassistant.local:9000/central
```

or, when using the Home Assistant IP address:

```text
ws://192.168.x.x:9000/central
```

## Operating Notes

Use `number.charger_maximum_current` for current control.

The Ocular charger has been tested changing between 10A, 13A, and 32A while
charging. Short OCPP reconnects should not stop charging; the charger continues
at the last accepted current until telemetry resumes.
