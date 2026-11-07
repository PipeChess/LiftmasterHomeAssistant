# 6 — Troubleshooting

| Symptom | Likely reason | What to verify |
|---|---|---|
| `Custom element doesn't exist: button-card` | Custom frontend resource not installed/loaded | Install [button-card](https://github.com/custom-cards/button-card) with HACS; confirm dashboard resource, refresh browser |
| Gate card status `STATUS UNKNOWN` | Wrong entity ID or unavailable text sensor | Check Developer Tools → States, update sample IDs in full YAML |
| Gate status always `Closed` | AUX input not switching, firmware pin mismatch, LiftMaster power loss | Test AUX contacts in a verified de-energized setup and D1/D2 contact closure separately; never equate OFF/OFF with independently verified security |
| D1 or D2 LED doesn't change when touching its input to **input GND** | Wrong terminal, GPIO or supply fault | Check terminal labels `D1…D4 GND`, KinCony manufacturer's pin table; no external voltage |
| D1 on, D2 off | Contradictory limit state | Inspect AUX programming, contacts, input inversion and wiring; suppress control if fault |
| Gate opens from Home Assistant Developer Tools but not dashboard | Button entity/action template not configured correctly | Compare `button.press` target with Developer Tools; check card JS syntax and current button-card version |
| Open/Close relay stays on | Raw relay exposed instead of momentary button configuration | Disconnect gate command wires and restore a tested 500 ms momentary configuration |
| Party Mode turns off after reboot | Expected from `restore_mode: ALWAYS_OFF` | Understand the gate may resume automatic closing; do not rely on this as a safety hold-open |
| Party Mode cannot be enabled | Gate not at **full open** position or invalid feedback | Check position sensor reports exact `Open`, D1/D2 both ON; don't bypass lockout to force state |
| Party Mode enabled but gate auto-closes | Wrong EXIT wiring, relay state or controller behavior | Verify dedicated main-board EXIT input, maintained dry-contact relay and all manufacturer controls with professional assistance |
| Lights don't update | Wrong light entity IDs / integration unavailable | Check two light entities in Developer Tools; use normal Hue integration, confirm `on`/`off` |
| Gate closes unexpectedly on controller disconnect | KinCony power loss released maintained EXIT hold | This is a design limitation. Evaluate supervised/independent hold-open solution with installer |
| Input LEDs behave but HA doesn't update | ESPHome disconnected/incorrect entity mapping | Check HA ESPHome integration and exact entities; compare physical LED with state |
| Unexplained movement during reboot | GPIO/relay startup transient | Disconnect gate interface; investigate hardware start behavior and fail-safe controls before further use |

## Diagnostic approach

1. Separate **physical relay behavior**, **ESPHome entity state**, and **dashboard behavior** rather than changing all three at once.
2. Test dry contacts with correct meter mode only on circuits proven voltage-free; never use continuity mode across a live voltage.
3. When changing wiring, isolate AC, backup battery, KinCony supply and verify zero energy; have gate technician perform/verify changes.
4. Do not disable or bypass safety devices to make a software command appear to work.
