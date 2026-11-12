# Troubleshooting

## Light never appears in Home Assistant

- Verify that Meross LAN was installed via HACS and Home Assistant was restarted.
- Check **Settings → Devices & services** for discovery notifications.
- Power-cycle the MSL420 for about ten seconds and check again, per Meross LAN guidance.
- Add **Meross LAN** manually if discovery fails. A Meross cloud profile can obtain the device key needed for communication.
- Ensure Home Assistant can reach the device over your home LAN, and check client isolation/VLAN firewall rules.

## Device is visible but cannot be controlled

- Confirm the entity ID is `light.*` and not a different domain.
- Make sure the entity is `available`, and try a simple `light.turn_on` action.
- Review Meross LAN's logs and transport options (AUTO / HTTP / MQTT).

## Script missing from Companion

- Open **Developer Tools → States** and find the actual `script.*` entity ID.
- In Home Assistant, run the script first. If YAML scripts were edited, reload scripts.
- Refresh/reconnect the Home Assistant connection in Bitfocus Companion.

## Feedback never changes

- Verify that the selected Companion variable is the light's *state*, with values `on` and `off`.
- Confirm changing the light from Home Assistant updates the state before debugging Companion.
- Remove a foreground image if it hides the Text style override.

## Security

Never publish HA tokens, Meross device keys, cloud account credentials, local hostnames/IPs, exported Companion configs with secrets, or your `secrets.yaml`.
