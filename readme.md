# BTT Relay 1.2 Firmware (modified)

User sobieh had changed the original firmware in his [repository](https://github.com/sobieh/bttrelay/) so that the relay doesn't need a reset but - and that made it unusable for me - he also changed a couple timeouts and the behaviour of the relay was modified so that it is enabled when the pin is pulled low. For regular cases (where the pc managing the printer is running 24/7) this makes sense but for mine (BTT E3EZ Board with a CB1 onboard) it doesn't.

## Firmware Description by sobieh

Modified BTT Relay 1.2 firmware for STC15F201S chip allowing to not only turn OFF the printer ... but also turn ON.
This feature was missing in original firmware and epic annoying, it required pushing Reset button every time you turn off the printer.
The modified firmware uses 3 seconds delay between ON/OFF or OFF/ON to avoid fast switching and sparking.

## Modifications by SirUli on top of sobieh's changes

- Shutdown Delay of 30 seconds (allows to shutdown a CB1 or CM4 embedded on your mainboard)
- Startup delay of 30 seconds (allows to start towards klipper without triggering a shutdown)
- Checks every 3 seconds for a changed pin (meaning that it can take up to 33 seconds to shutdown your relay)
- Enabled when Pin is pulled High

## Warning

`This device operates at mains voltage 230v!`
`You are using this software on your own risk.`

## Implementation

Short instructions below, see full instructions at: http://wolf-u.li/en/bigtreetech-relay-1.2-change-timeout-and-enable-turning-on-by-pin

### Build

- Download and install KEIL C51 (uVision) toolchain
- Add directory containing C51.exe to your PATH
- Run ``build.bat``

### Upload

- Install python 3.x
- `pip install stcgal`
- Connect your board to any USB to Serial adapter
- Run ``upload.bat COM#`` where # is your COM port number
- Reset the board with reset button
