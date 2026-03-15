# Sofle Keyboard

![SofleKeyboard version 1](https://i.imgur.com/S5GTKth.jpeg)

Sofle is 6×4+5 keys column-staggered split keyboard. Based on Lily58, Corne and Helix keyboards.

More details about the keyboard and build guides can be found here: [Sofle Keyboard Build Log and Guide](https://josefadamcik.github.io/SofleKeyboard)

* Keyboard Maintainer: [Josef Adamcik](https://josef-adamcik.cz) [Twitter:@josefadamcik](https://twitter.com/josefadamcik)  
* Hardware Supported: SofleKeyboard PCB, ProMicro  
* Hardware Availability: [PCB & Case Data](https://github.com/josefadamcik/SofleKeyboard)

## Firmware Revisions
- `sofle/rev1` is used for v1, v2, and RGB PCBs (**NOT** RGB PCBs purchased from [Keyhive](https://keyhive.xyz))
- `sofle/keyhive` is used for PCBs purchased from [Keyhive](https://keyhive.xyz/shop/sofle)
- [`keyboards/sofle_choc`](../sofle_choc/) is used for Choc PCBs

Make example for this keyboard (after setting up your build environment):

    make sofle/rev1:default
    make sofle/keyhive:default

Flashing example for this keyboard:

    make sofle/rev1:default:flash
    make sofle/keyhive:default:flash

Press reset button on he keyboard when asked.

Disconnect the first half, connect the second one and repeat the process.

See the [build environment setup](https://docs.qmk.fm/#/getting_started_build_tools) and the [make instructions](https://docs.qmk.fm/#/getting_started_make_guide) for more information. Brand new to QMK? Start with our [Complete Newbs Guide](https://docs.qmk.fm/#/newbs).

## bruno_becker Keymap Workflow

### Convert QMK Configurator JSON to keymap.c

Export your keymap from [QMK Configurator](https://config.qmk.fm) as a `.json` file, then convert it:

    qmk json2c sofle_v2_bruno.json -o keyboards/sofle/rev1/keymaps/bruno_becker/keymap.c

### Compile the firmware

    qmk compile -kb sofle/rev1 -km bruno_becker

The output file will be `.build/sofle_rev1_bruno_becker.hex`.

### Flash the firmware

Connect the keyboard via USB, then run:

    qmk flash -kb sofle/rev1 -km bruno_becker

When prompted `Waiting for USB serial port - reset your controller now`, press the reset button on the keyboard (briefly double-tap the button near the TRRS connector on the Pro Micro). Repeat the process for the second half.

### Dependencies (macOS)

If `qmk` is not found, install it and add it to PATH:

    pip3 install qmk
    echo 'export PATH="$PATH:/Users/$(whoami)/Library/Python/3.9/bin"' >> ~/.zshrc && source ~/.zshrc

If `avrdude` or `avr-gcc` are missing:

    brew install avrdude avr-gcc dos2unix

## Bootloader

Enter the bootloader in 3 ways:

* **Bootmagic reset**: Hold down the key at (0,0) in the matrix
* **Physical reset button**: Briefly press the button near the TRRS connector. Quickly double-tap if you are using Pro Micro.
* **Keycode in layout**: Press the key mapped to `QK_BOOT` if it is available
