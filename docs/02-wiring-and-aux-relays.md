# 2 — Wiring and auxiliary relays

> [!CAUTION]
> Gate-side electrical work must be performed or verified by a **trained gate-systems technician** with appropriate isolation/testing. This is a **functional wiring map for documentation**, not a substitute for the approved manual. Do not bypass any monitored safety, STOP, reset, photoeye, or edge device.

## Signals used

**Command direction**: KC868-A4 dry-contact relay closes across an approved LiftMaster input and its command common. **No voltage is injected** from the KinCony into LiftMaster command terminals.

| KC868-A4 | LiftMaster | Purpose | Contact behavior |
|---|---|---|---|
| Relay 1 `NO` + `COM` | Expansion board **green** `OPN+` + control `COM−` | Request open | Short momentary closure (~500 ms) |
| Relay 2 `NO` + `COM` | Expansion board **green** `CLS+` + same control `COM−` | Request close | Short momentary closure (~500 ms) |
| Relay 3 `NO` + `COM` | **Main** board's dedicated two-terminal `EXIT` + `COM` pair | Party Mode (hold open) | Maintained closure until disabled |

The expansion-board **green control COM** is shared by OPN/CLS/SBC/STP. The **yellow safety input COM is not an acceptable substitute** merely because its label also contains `COM`. Do not remove or defeat the existing `STP` to green `COM−` jumper. Distribute the returns using a correctly rated insulated splice/terminal rather than squeezing multiple wires under an unapproved terminal screw. Keep these command circuits electrically separate from the KC868 power supply and input GND.

The `EXIT` pair is on the **main control board**, not the expansion board; it is a soft open input that, when maintained at the open limit, pauses Timer-to-Close without disabling external entrapment protections. **Do not use `FIRE DEPT OPEN`: it has different behavior and may override external safeties.**

Relay 4 remains **unused**. The expansion board's `STP` contact is a **normally closed circuit**, not a third momentary NO input. Do not remove the stop jumper or wire Relay 4 without a separate, professionally verified design.

## AUX relay feedback

The expansion board has **two programmable AUX dry-contact relays** with `NO`, `COM`, `NC` terminals. The example uses `NO` and `COM` only.

| LiftMaster dry contact | KC868-A4 digital input | Meaning |
|---|---|---|
| AUX Relay 1 `NO` | `D1` (GPIO36) | Open-limit reached |
| AUX Relay 1 `COM` | Digital Input `GND` | Return |
| AUX Relay 2 `NO` | `D2` (GPIO39) | Away from closed limit |
| AUX Relay 2 `COM` | Digital Input `GND` | Return |

Use an appropriately rated insulated splice/distribution point for the two AUX COM return wires into the KinCony **digital-input** GND. Do **not** join that GND to LiftMaster's OPN/CLS command `COM−` just because both have common/ground markings. Do not inject external 12 V into the KinCony digital inputs: the intended input activation is a **dry-contact closure to its own input GND**.

### AUX switch settings used in the tested installation

| Expansion relay | Switch 1 | Switch 2 | Switch 3 | Function |
|---|---|---|---|---|
| AUX 1 | OFF | OFF | **ON** | **Open Limit**: energizes at open limit |
| AUX 2 | OFF | **ON** | OFF | **Close Limit/Not Closed**: energizes whenever gate is away from close limit |

The same functions appear in LiftMaster's expansion board AUX tables. Verify against the correct model/board version and **verify the resulting contact behavior with proper test equipment**. Switches for `EYE/EDGE`, Quick Close, Anti-Tailgate, BATT/EXIT fail functions, etc. are **not** part of this project and must remain in the manufacturer-prescribed states.

### Expected states

| Gate | AUX1 NO-COM | AUX2 NO-COM | D1 | D2 | ESPHome position |
|---|---|---|---|---|---|
| Closed at limit, controller healthy | open | open | OFF | OFF | `Closed`* |
| Between limits (either direction or stopped) | open | closed | OFF | ON | `Between Limits` |
| Fully open | closed | closed | ON | ON | `Open` |
| Impossible/contradictory relay state | closed | open | ON | OFF | `Invalid State` |

`*` **Important:** On loss of LiftMaster power or board/harness failure, both AUX relays can go inactive and falsely indicate `Closed`. Two dry-contact limit indications alone are **not fail-safe closure verification**. Add independent power/health monitoring and a validated fault strategy before using this for security or unattended automations.

## Suggested conductor plan

A **12-conductor** stranded cable provides ten signal conductors plus two spares. Colors are *local installation choices*, not a standard. Label **both ends** and identify them by terminal and continuity, not appearance.

```text
R1 NO   → OPN+                 1
R1 COM  → expansion COM−       2
R2 NO   → CLS+                 3
R2 COM  → expansion COM−       4
R3 NO   → main EXIT           5
R3 COM  → main EXIT COM       6
AUX1 NO → KinCony D1          7
AUX1 COM→ KinCony DI GND      8
AUX2 NO → KinCony D2          9
AUX2 COM→ KinCony DI GND     10
SPARE                         11
SPARE                         12
```

Where multiple conductors share one terminal, use a listed/approved distribution method as assessed by the installer. The manufacturer harness connecting expansion and main boards is **separate** from these signal wires.

## Sequence of work

1. Verify safe isolation of AC **and backup batteries**, and KinCony 12 V, before connecting anything.
2. Wire/verify the AUX feedback first, keep the command wires insulated and disconnected, and restore power to observe feedback using the existing original operator controls.
3. Verify NO/COM contact behavior for each command relay on the *disconnected* KinCony with a meter; confirm 500 ms pulse vs. maintained Party Mode.
4. Only after technician review and safety commissioning, connect and test Open, Close, then EXIT hold one at a time, with the gate visible and the area clear.
5. Re-test all original safeties, control access, and power-failure behavior before reliance.

See [commissioning checklist](05-testing-and-commissioning.md).
