#G3-TunR-V2
Browser tuner for the Ninebot Max G3. Region unlock and up to 50 km/h over Bluetooth — no app, no account, nothing installed.

Targets **MCU 1.6.0** and **VCU 1.6.3**; supports VCU **1.5.8 – 1.6.x**.

## Deploy (GitHub Pages)

1. New public repo → upload `index.html` and this README.
2. Settings → Pages → Source: *Deploy from a branch* → `main` / `root` → Save.
3. Open `https://<user>.github.io/<repo>/` on the phone in Chrome. HTTPS is required for Bluetooth.

## Use

1. Power on, close the Segway app completely.
2. Connect → pick the scooter → press its power button once.
3. **Backup** the serial number. Then pick region `C` (US), set 50, Apply.
4. Rebind the scooter in the Segway app afterwards — the SN is what it's bound to.

## What it writes

| Function | Where |
| --- | --- |
| Serial number / region | VCU cmd `0x18`, reg `0x10` |
| Speed caps | regs `0x45`, `0x46` |
| Cruise, TCS, units | reg `0x1D` bits 12/0/3 |
| KERS, acceleration, start speed, alarm | regs `0x70`, `0x6E`, `0x42`, `0x74` |
| Underglow, breathing tail, auto headlight | reg `0x1F` bits 2/1/0 |

Every write is read back. Writes are blocked unless the scooter is standing still.

## Notes

- `C` is the known US/unlocked region code. 50 km/h is above the US cap of ~40 — some MCU builds hold lower, that's the hardware, not the tool.
- iOS: Safari has no Web Bluetooth. Use the Bluefy browser.
- If a write fails, restore the backed-up SN and reboot. The ST-Link route still exists as a fallback.

MIT.
