# Eubanks Communications LTD — Meross MSL420 Stream Deck Control

Control a Meross MSL420 smart ambient light from an Elgato Stream Deck using **Bitfocus Companion → Home Assistant → Meross LAN → MSL420**.

> **Status:** Configuration starter project. The example YAML has not been tested against your physical light. Replace the placeholder entity ID before use.

## Features

- Power toggle and explicit on/off
- Brightness up/down (10 percentage points per press)
- RGB preset colours: red, blue, green
- Warm white, cool white and night mode presets
- Optional Companion feedback for live light on/off state

## 1. Add your MSL420 to Home Assistant

The third-party [Meross LAN integration](https://github.com/krahabb/meross_lan) explicitly lists MSL420 among supported lights. Its documentation says it can communicate over LAN HTTP and MQTT and can coexist with a device paired to the official Meross app. **Support can vary by firmware and network configuration.**

1. In Home Assistant install [HACS](https://www.hacs.xyz/) if needed.
2. In HACS search for **Meross LAN** and install it, then restart Home Assistant.
3. Navigate to **Settings → Devices & services**; configure a discovered Meross device, or choose **Add Integration → Meross LAN**.
4. When prompted, set up a Meross cloud profile or supply the **device key** and host IP, as explained in the upstream integration's README. Keep passwords, device keys and tokens out of this repository.
5. Find your light's actual entity ID in **Developer Tools → States** (e.g., `light.meross_msl420`). Test `light.toggle` before moving on.

**Do not remove the device from Apple Home just to try Meross LAN.** If choosing the HomeKit Device integration instead, review Home Assistant's current HomeKit Device guidance: already-paired accessories may need to be unpaired from Apple Home and re-exposed via HomeKit Bridge afterwards.

## 2. Install the Home Assistant scripts

The file [`home-assistant/scripts.yaml`](home-assistant/scripts.yaml) contains script definitions to merge **under the top level of an existing `scripts.yaml`**. Do not replace unrelated scripts.

1. Find your actual `light.` entity in **Developer Tools → States**.
2. In the YAML file replace every `light.meross_msl420` with the actual ID.
3. If you already use the YAML-based scripts configuration, **merge** each script definition into `scripts.yaml` and reload scripts from **Developer Tools → YAML → Reload Scripts** (or restart Home Assistant).
4. Alternatively, use the visual script editor and reproduce actions one by one, using [`docs/visual-editor.md`](docs/visual-editor.md).
5. Test each script from Home Assistant before connecting Companion.

The YAML is intentionally *not* a custom integration or a full Home Assistant configuration. Its scripts require the standard HA `light` domain and a working Meross light entity.

## 3. Configure Bitfocus Companion

See [`docs/companion-setup.md`](docs/companion-setup.md) for the full suggested 3 × 3 button map and feedback instructions.

For each Stream Deck key: **Buttons → Press actions → + Add action → Home Assistant → Execute script**, then choose the corresponding script entity. The exact script ID can be found in **Developer Tools → States**.

## 4. Safety and privacy

- Keep Home Assistant secrets, Meross account credentials, device keys and API tokens out of GitHub.
- The examples never expose a Meross key or hardcode a home IP.
- Brightness and RGB services only work when the light entity exposes those capabilities.
- Device status in Companion may lag slightly behind app/physical changes, depending on Meross LAN polling/transport.

## Project structure

```text
home-assistant/scripts.yaml    Example scripts to merge into your HA scripts
home-assistant/test-actions.yaml  Manual Developer Tools action examples
docs/visual-editor.md          No-YAML setup
docs/companion-setup.md        Button map and feedback configuration
docs/troubleshooting.md        Common pairing and entity issues
assets/button-map.svg         Optional reference image
```

## Upstream references

- [Meross LAN](https://github.com/krahabb/meross_lan)
- [Home Assistant Light integration](https://www.home-assistant.io/integrations/light/)
- [Home Assistant Scripts](https://www.home-assistant.io/integrations/script/)
- [Bitfocus Companion](https://companion.free/)

This is an independent setup guide, not an official Meross, Bitfocus or Home Assistant product.
