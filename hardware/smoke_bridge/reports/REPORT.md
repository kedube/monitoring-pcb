# Smoke/CO alarm Wi-Fi + Matter bridge (ESP32-C6, 120 VAC)

**Status:** NEEDS WORK

| | |
|---|---|
| Project | `/Users/katherine/Downloads/github/monitoring-pcb/hardware/smoke_bridge/smoke_bridge.kicad_pro` |
| Design spec | `/Users/katherine/Downloads/github/monitoring-pcb/hardware/smoke_bridge.json` |
| Board | 64 x 38 mm, 2 layers, 31 parts, 21 nets |
| Routing | signal-width power tracks, both layers free; 20 vias; 140.0 mm of signal on the bottom layer |
| Layout score | 97/100 compared with real 2-layer boards |
| ERC | no errors |
| DRC | 0 errors, 0 unconnected |
| Schematic vs board | match |
| Noise checks | 7 pass, 9 warn, 1 fail |
| Manufacturing files | `fab/smoke_bridge-gerbers.zip`, `fab/smoke_bridge-bom.csv`, `fab/smoke_bridge-cpl.csv`, `fab/smoke_bridge.step` |
| Time | check 0s, build 4s, preflight 0s, route 90s, fab 2s |

## Power

- power: U4 (AP2112K-3.3) 5V->3.3V at 150 mA dissipates 0.26 W; SOT-23 handles about 0.3 W
- rail +3V3 carries about 150 mA
- rail +5V carries about 151 mA

## Blocking

- noise: B.Cu pour covers 43% of the board

## Worth checking

- noise: U4.1 (VIN, net +5V): decoupling cap C14 is 2.9 mm pad-to-pad (aim for < 2.5 mm)
- noise: F.Cu pour covers 35% of the board, split into 4 islands
- noise: 140 mm of signal track on the bottom layer: each cut forces return currents around it; move routes to the top or use 4 layers
- noise: USB_DP: 23 mm, 3 vias -- 3 vias
- noise: USB_DP/USB_DN: 22.6 / 22.4 mm -- via count differs (3 vs 2)
- noise: +3V3 narrowest track 0.19 mm: thin supply traces add resistance and noise; widen where current flows
- noise: +5V narrowest track 0.25 mm: thin supply traces add resistance and noise; widen where current flows
- noise: HLK_5V narrowest track 0.25 mm: thin supply traces add resistance and noise; widen where current flows
- noise: VBUS_IN narrowest track 0.19 mm: thin supply traces add resistance and noise; widen where current flows
- J1: footprint smoke_bridge:Terminal_3P_5.08_L-N-IC does not match symbol's filters (TerminalBlock*:*) -- double-check the package
- RV1: footprint Capacitor_THT:C_Disc_D7.5mm_W5.0mm_P5.00mm does not match symbol's filters (RV_* Varistor*) -- double-check the package
- PS1: footprint smoke_bridge:HLK-PM01_IsolationBarrier does not match symbol's filters (Converter*ACDC*Hi?Link*HLK?PM*) -- double-check the package

## Next

- Open in KiCad: `open "/Users/katherine/Downloads/github/monitoring-pcb/hardware/smoke_bridge/smoke_bridge.kicad_pro"`
- Order boards: upload `fab/smoke_bridge-gerbers.zip`; for assembly also the BOM and CPL files
