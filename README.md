# hejnas-tripod-sensor

Open-source Bluetooth LE sports sensor: **one device, three mounts**. Works as a running foot pod, a crank cadence sensor or a wheel speed sensor, depending on which adapter it is mounted in.

| Mount | Measures | BLE profile |
|---|---|---|
| Shoe (laces) | Running cadence (also cycling cadence from the shoe) | RSC – Running Speed and Cadence (0x1814) |
| Crank arm | Cycling cadence | CSC – Cycling Speed and Cadence (0x1816), crank data |
| Wheel hub | Wheel speed and distance | CSC (0x1816), wheel data |

Battery level is exposed via the standard Battery Service (0x180F).

## Hardware

- [Seeed Studio XIAO MG24 Sense](https://wiki.seeedstudio.com/xiao_mg24_getting_started/) (Silicon Labs EFR32MG24, Cortex-M33, BLE 5.3)
- On-board 6-axis IMU: LSM6DS3TR-C
- LiPo battery, 210 mAh
- 3D-printed adapters (shoe / crank / hub)

## Target devices

Any watch or app supporting standard BLE RSC/CSC sensors. Primary test devices: Suunto Peak Pro and Suunto Vertical.

## Status

Early planning – no firmware yet. See the [roadmap](ROADMAP.md) for stages and progress.

## License

[MIT](LICENSE)
