# Quantum Mechanical Keyboard Firmware

[![Current Version](https://img.shields.io/github/tag/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/tags)
[![Discord](https://img.shields.io/discord/440868230475677696.svg)](https://discord.gg/qmk)
[![Docs Status](https://img.shields.io/badge/docs-ready-orange.svg)](https://docs.qmk.fm)
[![GitHub contributors](https://img.shields.io/github/contributors/qmk/qmk_firmware.svg)](https://github.com/qmk/qmk_firmware/pulse/monthly)
[![GitHub forks](https://img.shields.io/github/forks/qmk/qmk_firmware.svg?style=social&label=Fork)](https://github.com/qmk/qmk_firmware/)

This is a keyboard firmware based on the [tmk\_keyboard firmware](https://github.com/tmk/tmk_keyboard) with some useful features for Atmel AVR and ARM controllers, and more specifically, the [OLKB product line](https://olkb.com), the [ErgoDox EZ](https://ergodox-ez.com) keyboard, and the Clueboard product line.

## Documentation

* [See the official documentation on docs.qmk.fm](https://docs.qmk.fm)

The docs are powered by [VitePress](https://vitepress.dev/). They are also viewable offline; see [Previewing the Documentation](https://docs.qmk.fm/#/contributing?id=previewing-the-documentation) for more details.

You can request changes by making a fork and opening a [pull request](https://github.com/qmk/qmk_firmware/pulls).

## Supported Keyboards

* [Planck](/keyboards/planck/)
* [Preonic](/keyboards/preonic/)
* [ErgoDox EZ](/keyboards/ergodox_ez/)
* [Clueboard](/keyboards/clueboard/)
* [Cluepad](/keyboards/clueboard/17/)
* [Atreus](/keyboards/atreus/)

The project also includes community support for [lots of other keyboards](/keyboards/).

## Maintainers

QMK is developed and maintained by Jack Humbert of OLKB with contributions from the community, and of course, [Hasu](https://github.com/tmk). The OLKB product firmwares are maintained by [Jack Humbert](https://github.com/jackhumbert), the Ergodox EZ by [ZSA Technology Labs](https://github.com/zsa), the Clueboard by [Zach White](https://github.com/skullydazed), and the Atreus by [Phil Hagelberg](https://github.com/technomancy).

## Official Website

[qmk.fm](https://qmk.fm) is the official website of QMK, where you can find links to this page, the documentation, and the keyboards supported by QMK.

---

## Sofle V2 - Configuração de Bruno Becker

### Estrutura do Projeto

| Arquivo | Descrição |
|---------|-----------|
| `keyboards/sofle/rev1/keymaps/bruno_becker/keymap.c` | Keymap principal (Código C) |
| `sofle_v2_bruno.json` | Export para QMK Configurator |
| `keyboards/sofle/rev1/keymaps/bruno_becker/config.h` | Configurações (RGB, Split, etc.) |
| `keyboards/sofle/rev1/keymaps/bruno_becker/rules.mk` | Features habilitadas |

### Características do Keymap

- **5 camadas**: QWERTY (0), Colemak DH (1), Símbolos/Números (2), Navegação/Atalhos (3), Numpad/Mídia (4)
- **2 LEDs RGB WS2812** (1 em cada lado) - Porta D3
- **2 Encoders (Knobs)**:
  - Esquerdo: Volume (Vol+ / Vol-)
  - Direito: Brilho RGB / Matiz (click alterna cor)
- **Master**: Lado direito (`MASTER_RIGHT`)

### Comandos para Compilar e Flashar

```bash
# Compilar
qmk compile -kb sofle/rev1 -km bruno_becker

# Compilar e flashar (automático)
qmk flash -kb sofle/rev1 -km bruno_becker

# Ou usando make
make sofle/rev1:bruno_becker
```

### Modo DFU (para entrar em bootloader)

1. **Método físico**: Pressione o botão reset no Pro Micro 2x rapidamente
2. **Método via keymap**: Pressione `Reset` na camada 3 (se configurado) ou use `QK_BOOT`

### Atualizar via JSON (QMK Configurator)

```bash
# Converter JSON para C
qmk json2c sofle_v2_bruno.json -o keyboards/sofle/rev1/keymaps/bruno_becker/keymap.c

# Depois compile normalmente
qmk compile -kb sofle/rev1 -km bruno_becker
```

### Como transformar o keymap.c de volta para .json
```bash
qmk c2json -kb sofle/rev1 -km bruno_becker -o sofle_v2_bruno_atualizado.json

# ou
qmk c2json -kb sofle/rev1 -km bruno_becker --no-cpp -o sofle_v2_bruno_atualizado.json
```

### Converter o JSON para C (Atualizar o Keymap)
```bash
qmk json2c sofle_v2_bruno.json -o keyboards/sofle/rev1/keymaps/bruno_becker/keymap.c
```

### Solução de Problemas

| Problema | Solução |
|----------|---------|
| Teclado não responde | Verifique cabo USB no lado **direito** (master) |
| Metade não funciona | Verifique conexão TRRS entre as metades |
| LEDs não acendem | Verifique jumper/solda no pino D3 |
| Encoder não funciona | Verifique solda nos pinos F4/F5 |

### Documentação QMK

- [Guia de início](https://docs.qmk.fm/#/newbs)
- [Comandos CLI](https://docs.qmk.fm/#/cli_commands)
- [Tap Dance](https://docs.qmk.fm/#/feature_tap_dance)
- [Encoders](https://docs.qmk.fm/#/feature_encoders)
