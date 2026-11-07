# 1 — Hardware inventory and mounting

## Confirm the exact model

This walk-through covers a LiftMaster **LA400DC** residential DC swing-gate operator with its compatible expansion board (**K1D8387-1CC**) and a KinCony **KC868-A4**. Models that look similar can have different terminals, safety requirements, power supplies, and accessory compatibility. Consult the *specific* installation manual first.

## Inventory

- Compatible LiftMaster expansion board, **factory interconnect harness**, mounting screws, and standoffs.
- KinCony KC868-A4 with suitable, safely mounted enclosure.
- Regulated **12 V DC** supply for the KinCony, with appropriate environmental rating and capacity.
- Insulated, appropriately rated multi-conductor stranded low-voltage cable (10 conductors used; 12 convenient).
- Insulated terminal distribution connectors, wire labels, strain relief, and proper mounting hardware.
- Multimeter; professional testing equipment for safety/entrapment devices.
- Existing factory safety devices and visible manual stop/reset controls must remain intact.

## Mechanical arrangement

The expansion board mounts inside the LiftMaster control box on its designated elevated posts/standoffs, and connects to the main board's `EXP BOARD` connection using the supplied harness. Some kits include a compatibility service bulletin for other LiftMaster products; **do not reverse supply polarity or modify other wiring based on a bulletin for a different operator**.

Place the KinCony in a protected enclosure within the operator housing only if permitted by the manufacturer and local installation requirements. Consider:

- Physical fasteners instead of adhesive-only hook-and-loop tape (heat/cold can weaken adhesive).
- Service slack and strain relief; no pinched wires when the enclosure closes.
- Clearance from moving hinges and cables, mains supply, motor leads and existing control circuits.
- Moisture/condensation and outdoor winter temperature ratings (one candidate UL2464 cable was rated only to −15 °C, which may be unsuitable for some winter installations).
- Wi-Fi reception with the metal or plastic control-box lid fully closed.
- A safe, code-compliant means to supply **12 V DC**; the LiftMaster accessory outputs are **24 V**, not interchangeable.

## Power and installation

**Installer/qualified technician required:** The manufacturer calls for installation and service by a trained gate-systems technician. Isolate **AC and both backup batteries**, verify de-energization, and follow all lockout, ESD and electrical practices before changing the operator wiring. On many LiftMaster controllers, disconnecting AC alone leaves the board energized from batteries.

Do not rely on this project to determine which mounting holes, screws, or power-supply conversion methods are legal for your installation. Have those reviewed in situ.

Next: [terminal functions and wiring](02-wiring-and-aux-relays.md).
