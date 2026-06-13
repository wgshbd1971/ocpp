# Supported Device

This fork is maintained for one charger:

```text
Ocular OC20-BC-7kW-PLUS-V3
```

Also known during testing as:

```text
Ocular 7kW Lite Plus
```

OCPP values seen from the charger:

```text
Vendor: Broadview
Firmware: 405.3251.0Q03196
Protocol: ocpp1.6
```

## Tested Behaviour

- Home Assistant can set charging current with `number.charger_maximum_current`.
- 10A, 13A, and 32A current profiles have been accepted and applied.
- The charger continues at the last accepted current through brief websocket
  reconnects.
- Home Assistant Core restart while charging has been tested.
- Charger power-cycle while plugged in and charging has been tested.

## Important Notes

This fork favours Ocular behaviour over general OCPP compatibility. Other
chargers may work, but they are not the target of this repository.

For general charger compatibility, use the upstream project:

```text
https://github.com/lbbrhzn/ocpp
```
