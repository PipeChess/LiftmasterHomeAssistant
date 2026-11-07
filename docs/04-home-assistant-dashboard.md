# 4 — Home Assistant dashboard

## Prerequisites

- ESPHome integration online and exposing button/switch/input/text-sensor entities.
- HACS and [custom:button-card](https://github.com/custom-cards/button-card) installed; verify the resource is loaded (HACS usually adds it automatically).
- Optional: two Hue gate-post light entities accessible through the Hue integration.

## Install the Lovelace card

1. In Home Assistant, go to **Developer Tools → States**. Record the exact entity IDs for `Gate Position`, `Gate Open`, `Gate Close`, `Gate Party Mode`, and optionally Left/Right lights.
2. Open [`home-assistant/driveway-gate-card.yaml`](../home-assistant/driveway-gate-card.yaml) and replace the sample entity IDs throughout with your own values. You can use editor **Find/Replace**.
3. Open dashboard → **Edit** → **Add Card** → **Manual**. Paste the whole YAML.
4. Validate the displayed status and lamps before testing command buttons. Keep a verified remote/STOP control available, and complete [commissioning](05-testing-and-commissioning.md) first.

The sample entity IDs are generic. They are NOT automatically created with exactly those strings: Home Assistant assigns IDs based on device friendly name, collisions and previous naming.

## Dashboard behavior

| Reported position | OPEN button | CLOSE button | Party Mode |
|---|---|---|---|
| `Closed` | Enabled, confirmation | Disabled | Cannot enable |
| `Between Limits` | Enabled, confirmation | Enabled, confirmation | Cannot enable |
| `Open` | Disabled | Enabled, confirmation | Can enable |
| `Invalid State`, `unavailable`, or `unknown` | Disabled | Disabled | Cannot enable |
| Party Mode currently ON | Position rules above | Position rules above | **Can always disable** |

All buttons are **visual controls, not safety interlocks**. The ESPHome example adds limit guards at the device level, but the gate's original controls, force/safety features and external inputs can still move it. Neither dashboard nor ESPHome is safety certified.

The illustration uses a stylized, arched **two-leaf wrought-metal gate** and lights on both posts. The two lamps glow warmly when their Home Assistant light entity reports `on`; they each have an ON/OFF toggle with long-press more-info (brightness support depends on the light). No photos of your actual residence are bundled.

## Optional example Hue lights

In the sample card, replace:

```yaml
light.gate_post_left
light.gate_post_right
```

with your own HA entities (or remove the light button `horizontal-stack` and the illustration's lamp entity references if you don't use them).

## Why the card doesn't show a true 0–100% position

AUX1 and AUX2 report the **limit states**, not encoder angle or direction. The illustrated partly open position is a *symbol for between limits*, not a measured percentage. No automatic stop command is included: the `STP` circuit requires different wiring, and should not be casually repurposed.

## Why an unknown/power-off status matters

If the main controller loses power but the KinCony remains online, AUX1/OFF + AUX2/OFF can still look like `Closed`. Do not label this as `Secure` or trigger garage security routines without an independent operator-health/closure confirmation.
