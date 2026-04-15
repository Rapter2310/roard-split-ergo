# Roard Keyboard

Roard is a custom wireless split keyboard I designed, heavily based on the Lily58. The main physical difference is the layout. I modified it to include a dedicated arrow key cluster on the right half. 

The biggest technical difference is the wireless setup. Instead of standard Bluetooth, I'm using a 3-node Nordic Enhanced ShockBurst (ESB) configuration. The left and right halves connect to a third nice!nano plugged into the PC acting as a dedicated dongle, which fixes the latency and connection drops you sometimes get with standard BLE splits.

## Hardware Details
* **Controllers:** 3x nice!nano v2 (left, right, and central dongle).
* **Displays:** 2x nice!view screens.
* **Switches & Sockets:** Gateron Aliaz (silent tactiles) seated in Kailh MX hotswap sockets.
* **Power:** 3.7v 110mAh LiPo batteries.
* **Components & Assembly:** Sourced all the board-level SMD components (diodes, power/reset switches, battery connectors, and sockets) directly from Typeractive, and assembled the board using Kester solder wire.
* **Design Tools:** The core layout was built in Keyboard Layout Editor (KLE). I initially used the ai03 plate generator for rapid prototyping to test different angles and ergonomics before committing to the board design. To map the final physical matrix to the firmware, I used the [ZMK Physical Layout Converter](https://zmk-physical-layout-converter.streamlit.app/) to translate the KLE JSON directly into ZMK layout macros. The raw design files are in the `/design` folder.
* **PCB:** Custom routed in KiCad. Once the routing and standoff placements were finalized, I exported the board as a STEP file to serve as the foundation for the mechanical design.

## Case & Mechanical
I modeled the enclosure from scratch in Onshape. To guarantee perfect switch alignment and mounting hole clearance, I imported the KiCad STEP file directly into my Onshape workspace and traced the final switch plates and case standoffs around the exact geometry of the PCB.

I used a few different materials for the 3D printed parts depending on what they needed to do:
* **Case & Switch Plate:** PETG for general strength.
* **Tenting Kit:** TPU so it actually grips the desk and dampens the sound a bit.
* **Display Covers:** PLA to protect the nice!view screens.
Everything is held together with standard brass standoffs.

## Current Status & WIP
The board is fully functional as my daily driver, but I'm currently working on two main things:

1. **Customizing the nice!view Screens:** Switching from standard BLE to the ESB dongle setup breaks the standard `nice!view` widget implementation, which relies on BLE Zephyr services to report full connection states. Currently, the screens are running a basic fallback ZMK display profile that only outputs battery levels. I am actively rewriting the display logic to pull layer information and connection states over the ESB protocol to restore full functionality.
2. **Custom Keycaps:** I'm in the process of generating and 3D printing a custom keycap profile using [PseudoMakeMeKeyCapProfiles](https://github.com/pseudoku/PseudoMakeMeKeyCapProfiles).

## Repository Structure
* `/design`: KLE json files and prototyping assets.
* `/docs`: Photos of the finished board, the PCB, and the tenting kit.
* `/firmware`: ZMK config files, custom shield definitions, and ESB dongle setup.
* `/hardware`: KiCad project files, schematics, and production-ready Gerbers.
* `/mechanical`: STLs for 3D printing and STEP files exported from Onshape.