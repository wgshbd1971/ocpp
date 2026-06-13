# Contribution Notes

This is a personal fork for an Ocular `OC20-BC-7kW-PLUS-V3` charger connected
to Home Assistant through OCPP 1.6.

General charger compatibility work should go to the upstream project:

```text
https://github.com/lbbrhzn/ocpp
```

Changes in this fork should stay focused on the tested Ocular/Broadview setup.

## Before Changing Integration Code

Check that the change preserves:

- Maximum-current control through `number.charger_maximum_current`.
- Startup and reconnect behaviour for the Ocular charger.
- Manual installation from `custom_components/ocpp`.
- Home Assistant tests and Hassfest validation.

## Local Checks

Run the same basic checks used by GitHub Actions:

```sh
pre-commit run --all-files
pytest --durations=10 --cov-report term-missing --cov=custom_components.ocpp tests
```

## License

This fork keeps the upstream MIT license.
