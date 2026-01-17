# 0bgk.keymap

Personal keymap configuration for KBD6x keyboard.

## Hardware

**KBD6x** - A 60% keyboard PCB with HHKB layout support (Atmega32u4)

## Keymap Features

HHKB-inspired layout optimized for Vim users with media controls.

**Layer 0:**
- CAPS position → `CTL_T(KC_ESC)` (tap ESC, hold Ctrl)
- Space → `LT(1, KC_SPC)` (tap Space, hold Fn)
- Fn key (right of Right Shift) → `TG(1)` (toggle Layer 1)

**Layer 1:**
- F1-F13 keys
- Vim arrows: H/J/K/L → ←/↓/↑/→
- Media: E/C (vol up/down), S/D/F (prev/play/next)

## Setup

```bash
# Install QMK
brew install qmk/qmk/qmk

# Setup QMK (clones firmware repo and configures environment)
qmk setup

# Copy keymap
cp -r /path/to/0bgk.keymap/keymaps/hhkb ~/qmk_firmware/keyboards/kbdfans/kbd6x/keymaps/

# Compile and flash
qmk flash -kb kbdfans/kbd6x -km hhkb
```

## Customization

Edit `keymaps/hhkb/keymap.c` and recompile. See [QMK Keycodes](https://docs.qmk.fm/keycodes) reference.

## License

GPL v2.0 - See [LICENSE](LICENSE) file.
