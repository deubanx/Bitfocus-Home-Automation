# Bitfocus Companion / Stream Deck configuration

Companion is already connected to Home Assistant in the intended setup. These steps re-use that connection.

## Suggested button map

| Row | Left | Middle | Right |
| --- | --- | --- | --- |
| 1 | Power toggle | Brighter (+10%) | Dimmer (−10%) |
| 2 | Red | Blue | Green |
| 3 | Night | Warm | White |

## Action mapping

| Button | Home Assistant script |
| --- | --- |
| Power | `script.meross_msl420_toggle` |
| Brighter | `script.meross_msl420_brighter` |
| Dimmer | `script.meross_msl420_dimmer` |
| Red | `script.meross_msl420_red` |
| Blue | `script.meross_msl420_blue` |
| Green | `script.meross_msl420_green` |
| Night | `script.meross_msl420_night` |
| Warm | `script.meross_msl420_warm` |
| White | `script.meross_msl420_white` |

In **Buttons**, choose the target key → **Press actions** → **+ Add action** → **Home Assistant → Execute script** → pick the actual script entity. Use the action names offered by your installed HA Companion module version.

## Style

In Companion 5, use **Style → + Add element → Text** and add labels such as `⏻`, `☀ +`, `☀ −`, `RED`, etc. Place text above background/image layers. Use `Style → + Add element → Image` for an imported icon PNG if preferred.

## Optional live power feedback

Use the same technique as the Apple TV Play/Pause button:

1. In **Feedbacks** choose **Internal → Variable: Check value**.
2. Select the Home Assistant **entity state** variable for your `light.` entity (not entity name or friendly name).
3. Operation `=`; Value `on`; Invert off.
4. Under **Style Overrides**, select the **Text** element and override its Color to green or yellow. Optionally override Background → Color.
5. In **Style**, set the default button colour to grey for when the light is off.

Test by switching the light on/off in the Meross app. Companion will reflect the state if the Home Assistant integration successfully reports state changes.

## Notes

- `rgb_color` services rely on RGB support exposed by Home Assistant; some firmware/device modes may behave differently.
- If you already have a working colour command, consider setting a scene for reliable repeatability.
- Never store credentials or API keys in your Companion exports if publishing them publicly.
