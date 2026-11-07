# 7 — Safety, security and privacy

## Physical safety is primary

This reference integrates a **vehicular** motorized swing gate. It does not certify the gate or absolve installers of relevant codes or the manufacturer's instructions. LiftMaster states this product is to be installed and serviced **only by a trained gate systems technician**. A working ESPHome button and confirmation dialog are not substitutes for a safety-rated circuit or supervised operation.

- Never disable, reroute, or bypass monitored entrapment inputs, photo eyes, sensing edges, STOP controls, or obstruction reversal.
- Do not use the **FIRE DEPT OPEN** contact as the Party Mode interface; the documented input may override external safeties. Use the *soft* EXIT function only when an installer has verified its operation and suitability.
- Separate KinCony power and digital input ground from LiftMaster command common. Never inject 12/24 V into a dry-contact control input.
- Verify both AC mains and backup battery power are disconnected before electrical service; have a technician do/approve gate-side wiring.
- Don't use continuity/ohms meter mode on an energized circuit. Secure test leads only after safe isolation; operate the gate while keeping everyone outside the moving area.
- Use proper cable ratings, rated connectors, environmental protection, strain relief, and hardware mounting. Don't assume a product is code compliant because it fits a connector.
- Keep the existing emergency stop and manual controls available and tested.
- A *CLOSE* button that can be pressed from anywhere is particularly sensitive. Meet local rules and monitored protection requirements before allowing remote or unattended closing.

## Important logical limitations

**False Closed possibility:** AUX relay 1 = OFF and AUX relay 2 = OFF is the *expected* powered/healthy closed-limit condition, **but also** occurs if the expansion board loses power. No independent power/health input is provided by this two-wire scheme; display `Closed limit indicated`, not guaranteed security.

**No measured travel angle or direction:** `Between Limits` is an inferred state from two limit contacts. Do not call it definitely `Opening` or `Closing` without additional verified inputs.

**Party Mode failure behavior:** Maintained KinCony Relay 3 holds the main-board EXIT. On KinCony power failure/reboot the relay releases; the gate's regular timer-to-close may then resume. Party Mode is not a guaranteed hold-open safety function.

**Software interlocks:** ESPHome GPIO `interlock` and `restore_mode: ALWAYS_OFF` do not guarantee safe behavior while the chip boots, crashes, or loses power. Use physical, manufacturer-compliant safeguards.

## Network security

- Use a protected local network and ESPHome API encryption.
- Keep Home Assistant accounts secured, with least necessary dashboard access.
- Prefer an authenticated VPN over exposing control UIs/ESPHome API ports directly to the public Internet.
- Prevent automations or voice assistants from opening/closing the gate without appropriate physical authorization and safeguards.
- Avoid publishing precise property photos, addresses, videos, live gate-camera URLs, credentials, API encryption secrets, network topology, or device IDs that identify the property.

## Publishing checklist

- [ ] `esphome/secrets.yaml` is excluded and replaced with `secrets.example.yaml`.
- [ ] No actual private Wi-Fi SSID/password, API encryption key, address, phone, serial or MAC identifiers.
- [ ] No private exterior house/gate photos or video feed endpoints without informed approval.
- [ ] The README clearly describes safety and power-loss limitations.
- [ ] Original third-party copyrighted manuals/firmware are linked, not copied into repository.
- [ ] Tested vs. example-only behavior is clearly labeled.
