# Debugging

To enable debug logging for this integration and related libraries, update
Home Assistant `configuration.yaml`:

```yaml
logger:
  default: info
  logs:
    custom_components.ocpp: debug
```

For low-level websocket messages, add:

```yaml
logger:
  default: info
  logs:
    custom_components.ocpp: debug
    websockets.server: debug
```

## Useful Commands

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
