# 0bgk.keymap

Personal keymap configuration for KBD6x keyboard.

## Hardware

**KBD6x** - A WKL (Winkeyless) Hot Swap Double USB C 60% keyboard

* Hardware Supported: KBD6x PCB
* Hardware Availability: [KBDFans](https://kbdfans.cn/products/kbd6x-wkl-hot-swap-60-double-type-c-pcb)

## Features

This configuration includes:
- Backlight support with breathing effect
- RGB underglow with 14 LEDs
- Multiple RGB animations (breathing, rainbow, snake, knight, etc.)
- Full NKRO support
- Bootmagic enabled

## Building

To compile this keymap for use with QMK:

1. Clone [QMK Firmware](https://github.com/qmk/qmk_firmware)
2. Copy this configuration to `keyboards/kbdfans/kbd6x/keymaps/0bgk/`
3. Build with: `make kbdfans/kbd6x:0bgk`

For more information, see the [QMK documentation](https://docs.qmk.fm/).

## Project Structure

```
.
├── keyboard.json      # Main keyboard configuration
├── keymaps/          # Keymap layouts
│   ├── default/
│   ├── hhkb-default/
│   └── hhkb-default-improved/
└── README.md
```

## License

This project is licensed under the GNU General Public License v2.0 - see the [LICENSE](LICENSE) file for details.

This configuration is derived from the [QMK Firmware](https://github.com/qmk/qmk_firmware) project.

## Original Maintainer

Original keyboard definition by [MechMerlin](https://github.com/mechmerlin)
