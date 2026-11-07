# 5 — Test and commissioning checklist

> [!WARNING]
> Follow the **specific LiftMaster manual** and engage a trained gate-system technician to commission gate-side connections and verify all UL325-required entrapment protections. Never use a person to test an obstruction or rely on this checklist instead of the official safety procedure.

## A. Before connecting to the gate

- [ ] Confirm correct operator/expansion-board models and the published connection manual.
- [ ] Mount hardware securely; no potentially pinched, rubbing or loose cables.
- [ ] Verify 12 V DC power polarity and current capability **with a meter**.
- [ ] Keep all command wires disconnected from the gate, individually insulated, and labeled.
- [ ] With KinCony disconnected from any other power source, verify NO/COM dry contacts: open while idle, short pulse for Open and Close, maintained closure for Party Mode.
- [ ] Verify the actual electrical behavior of all four D inputs using a dry contact to the KC868 input GND. No external voltage.
- [ ] Reboot the KinCony while disconnected from the gate; observe potential relay glitches, confirm all outputs are OFF after startup.
- [ ] Preserve all factory connections, monitored entrapment devices and STOP jumper.

## B. Expansion board AUX relays only

- [ ] Technician has isolated AC **and backup batteries**, wired/verified AUX1/AUX2 to digital input D1/D2, inspected terminal torque and strain relief.
- [ ] With power safely restored and everyone clear, close gate using **existing factory operator controls**: HA D1 OFF / D2 OFF.
- [ ] Open with existing controls: D1 OFF → D2 ON while between limits, then D1 ON / D2 ON at full open.
- [ ] During closing: D1 returns OFF before/while gate departs open limit, D2 remains ON until fully closed, then both OFF.
- [ ] Check any impossible combination (D1 ON, D2 OFF) is displayed as a fault.
- [ ] Document **false Closed risk** if controller loses power or AUX output fails. Don't claim fail-safe closure.

## C. Gate control commissioning

These tests must be overseen by a trained gate-systems technician with the gate **continuously visible** and the area fully clear.

- [ ] Verify command relay inputs OPN and CLS and their **green command COM**, not yellow safety COM.
- [ ] Verify STOP wiring/jumper and all original emergency controls still work.
- [ ] Verify Open request from HA produces one intended opening request and never keeps its relay latched.
- [ ] Verify Close request produces one intended closing request and never keeps its relay latched.
- [ ] Confirm the UI requires Open/Close confirmation and disables redundant command at the respective limit.
- [ ] Verify the device-level example also rejects Open at open limit and Close at closed limit (if using hardened reference firmware).
- [ ] Verify Relay 3 is across the **main board EXIT/COM**, not FIRE DEPT OPEN; enabling while fully open holds gate open past the normal closing interval.
- [ ] Verify Party Mode can only be enabled at full open via approved controls, and can always be disabled.
- [ ] Verify that disabling Party Mode releases the maintained EXIT hold and expected timer/close behavior resumes.
- [ ] Test KinCony disconnect/reboot with gate held open: understand that EXIT hold drops out and gate may auto-close. Decide whether this is acceptable **before** depending on Party Mode.
- [ ] Test loss of Wi-Fi / HA / mains and battery-borne behavior. Record limits of the solution.

## D. Mandatory gate safety verification

- [ ] Technician verifies **all manufacturer-required monitored photo eyes, edge sensors and inherent reversal protection**, under the full test procedure and relevant local requirements.
- [ ] Verify existing reset and stop functions are accessible and functional.
- [ ] Ensure remote closing is permitted and appropriately protected for the actual site; if not, **do not expose a remote CLOSE command**.
- [ ] Verify weatherproofing, enclosure close, wiring support, corrosion protection, low-temperature ratings and any required labeling.
- [ ] Arrange periodic safety tests following the official LiftMaster maintenance schedule.

Do **not** test entrapment with people or hands. Follow only the manufacturer-prescribed procedure and tools with a qualified professional.
