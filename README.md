# 0bgk.keymap

Personal keymap configuration for KBD6x keyboard.

## Hardware

**KBD6x** - A WKL (Winkeyless) Hot Swap Double USB C 60% keyboard

* Hardware Supported: KBD6x PCB
* Hardware Availability: [KBDFans](https://kbdfans.cn/products/kbd6x-wkl-hot-swap-60-double-type-c-pcb)

## Keymap Features

### HHKB Layout

Custom HHKB-inspired layout optimized for Vim users with media controls:

**Layer 0 (Base Layer):**
- **CAPS position** → `CTL_T(KC_ESC)`: Tap for ESC, Hold for Control
- **Space** → `LT(1, KC_SPC)`: Tap for Space, Hold for Layer 1 (Fn)
- CAPS in top-left position
- Standard QWERTY layout
- Right Shift doubles as TG(1) - toggle Layer 1 permanently
- Optimized tap-hold timing (200ms for Space/Fn, 150ms for Ctrl/ESC) to prevent accidental layer activation while typing

**Layer 1 (Function Layer)** - Hold Space to activate:
- F1-F13 and Print on top row
- **Vim-style arrow keys**: H (←), J (↓), K (↑), L (→)
- **Media controls**:
  - E: Volume Up
  - S: Previous Track
  - D: Play/Pause
  - F: Next Track
  - C: Volume Down
- LCTL and RCTL available on bottom corners
- DELETE on top-left

### Hardware Features

- Backlight support with breathing effect
- RGB underglow with 14 LEDs
- Multiple RGB animations (breathing, rainbow, snake, knight, etc.)
- Full NKRO support
- Bootmagic enabled

## Prerequisites

### macOS

Install QMK CLI and dependencies:

```bash
brew install qmk/qmk/qmk
```

This will automatically install:
- avr-gcc, avr-binutils (for AVR chips)
- arm-none-eabi-gcc, arm-none-eabi-binutils (for ARM chips)
- dfu-programmer, dfu-util, avrdude (for flashing)
- Python and QMK CLI tools

### Other Platforms

See [QMK Setup Guide](https://docs.qmk.fm/#/newbs_getting_started)

## Building

### 1. Setup QMK

Clone QMK Firmware:

```bash
# Clone QMK firmware
git clone https://github.com/qmk/qmk_firmware.git
```

### 2. Install Your Keymap

Copy your keymap to QMK:

```bash
# Initialize submodules (first time only)
cd qmk_firmware
git submodule update --init --recursive

# Copy HHKB layout
cp -r /path/to/0bgk.keymap/keymaps/hhkb keyboards/kbdfans/kbd6x/keymaps/
```

### 3. Compile Firmware

```bash
# Compile HHKB layout
qmk compile -kb kbdfans/kbd6x -km hhkb

# The compiled firmware will be at:
# qmk_firmware/kbdfans_kbd6x_hhkb.hex
```

## Flashing

### Method 1: Automatic Flash (Recommended)

```bash
# Start the flash process
qmk flash -kb kbdfans/kbd6x -km hhkb

# Follow the bootloader instructions (see below)
```

### Method 2: Manual Flash

```bash
# 1. Compile first
qmk compile -kb kbdfans/kbd6x -km hhkb

# 2. Put keyboard in bootloader mode (see below)

# 3. Flash with dfu-programmer
dfu-programmer atmega32u4 erase
dfu-programmer atmega32u4 flash kbdfans_kbd6x_hhkb.hex
dfu-programmer atmega32u4 reset
```

### Entering Bootloader Mode

The KBD6x uses **Atmel DFU** bootloader. To enter bootloader mode:

**Option 1: Bootmagic**
1. Disconnect keyboard
2. Hold down the **top-left key** (CAPS in our layout)
3. Plug in USB cable while holding
4. Release after 1 second

**Option 2: Physical Reset Button**
- Some KBD6x PCBs have a reset button on the back
- Press it while keyboard is connected

**Option 3: Keycode Reset**
- If you have QK_BOOT mapped, press it

When in bootloader mode, the `qmk flash` command will detect it automatically and flash the firmware.

## Project Structure

```
.
├── keyboard.json      # Main keyboard hardware configuration
├── keymaps/
│   └── hhkb/         # Custom HHKB layout with Vim navigation and media controls
│       └── keymap.c  # Main keymap configuration
├── LICENSE           # GPL v2.0 License
└── README.md         # This file
```

## Customization

To customize your keymap:

1. Edit `keymaps/hhkb/keymap.c`
2. Modify the key mappings in the `keymaps` array
3. Adjust tap-hold timing in `get_tapping_term()` if needed (default: 150ms)
4. Recompile and flash

### Common Keycodes

- `KC_TRNS` - Transparent (use key from lower layer)
- `LT(layer, kc)` - Tap for keycode, hold for layer
- `CTL_T(kc)` - Tap for keycode, hold for Control
- `TG(layer)` - Toggle layer on/off
- `MO(layer)` - Momentary layer while held
- `KC_ESC`, `KC_TAB`, `KC_BSPC` - Standard keys
- `KC_LSFT`, `KC_RSFT` - Shift keys
- `KC_LEFT`, `KC_DOWN`, `KC_UP`, `KC_RGHT` - Arrow keys
- `KC_MPRV`, `KC_MPLY`, `KC_MNXT` - Media previous/play/next
- `KC_VOLU`, `KC_VOLD` - Volume up/down

See [QMK Keycodes](https://docs.qmk.fm/#/keycodes) for full reference.

## Troubleshooting

### Keyboard not detected in bootloader mode
- Try different USB cable
- Use USB 2.0 port (not USB-C to USB-C on some Macs)
- Make sure you're holding the correct key (top-left)

### Flash fails
- Ensure dfu-programmer is installed: `brew list | grep dfu`
- Check keyboard is in bootloader: `dfu-programmer atmega32u4 get bootloader-version`

### Keys not working as expected
- Verify you flashed the correct keymap
- Check the keymap file has correct layer definitions
- Test in [QMK Configurator](https://config.qmk.fm/#/test)

## Resources

- [QMK Documentation](https://docs.qmk.fm/)
- [QMK Configurator](https://config.qmk.fm/)
- [KBDFans Discord](https://discord.gg/kbdfans)
- [r/MechanicalKeyboards](https://reddit.com/r/MechanicalKeyboards)

## License

This project is licensed under the GNU General Public License v2.0 - see the [LICENSE](LICENSE) file for details.

This configuration is derived from the [QMK Firmware](https://github.com/qmk/qmk_firmware) project.

## Credits

- Original keyboard definition by [MechMerlin](https://github.com/mechmerlin)
- Custom HHKB layout by 0bgk
