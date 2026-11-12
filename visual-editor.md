# Set up without YAML — Home Assistant visual editor

This path avoids the common `Message malformed: not a valid option at 'states[0].alias'` error from pasting an entire script into an individual action editor.

1. Navigate to **Settings → Automations & scenes → Scripts → Create script → Create new script**.
2. Name it **Meross MSL420 Toggle**.
3. In **Sequence**, choose **Add action**.
4. Select **Light: Toggle**, choose your actual Meross light entity, then save.
5. Open your saved script and **Run** it. If the light turns on/off, it is ready for Companion.
6. Repeat with **Light: Turn on** for Red, Blue, Green, Warm, White and Night, using the preset colours from `scripts.yaml`. Repeat with **Light: Turn off** if you'd like a dedicated off key.

## Brightness buttons

For **Meross MSL420 Brighter**, select **Light: Turn on**. If the visual editor exposes **Brightness step percent**, use `10`. For **Dimmer**, use `-10`. If it does not, use **Edit action in YAML**, pasting only the action object:

```yaml
action: light.turn_on
target:
  entity_id: light.meross_msl420
data:
  brightness_step_pct: 10
```

Do not paste `alias:` or `sequence:` into an action editor. Replace the example entity ID.

## Validate

Go to **Developer Tools → States** and search `script.meross_msl420_toggle`. Home Assistant may add a numeric suffix to the ID; use the actual ID shown.
