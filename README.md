# screen-real-size

**Calibrate your screen's real pixel/mm ratio using a credit card.**

Ever designed a UI for a small screen (Nextion, Raspberry Pi, etc.) and realized the dimensions didn't match when deployed? This tool solves that by calibrating your PC monitor's actual pixel-to-millimeter ratio using a standard credit card (ISO/IEC 7810 ID-1: 85.6mm x 53.98mm) as a physical reference.

## Live Demo

**[Try it now](https://umitkosa.github.io/screen-real-size/)**

No download, no install. Just open the link, place your credit card on the screen, and calibrate.

## How It Works

1. Open the calibration page in your browser (zoom must be 100%)
2. Place your credit card on the screen
3. Adjust the slider until the frame matches your card exactly
4. Click **Confirm**
5. Copy the auto-generated prompt and paste it into **Claude Code**

That's it. Claude Code now knows your screen's exact pixel/mm ratio and will design all UI elements at their real physical dimensions.

## Features

- **Credit card reference** - Uses the worldwide ISO 7810 standard (85.6 x 53.98mm)
- **Precision mode** - 1x and 1/5x slider speed for fine-tuning
- **2 themes** - Dark Blue and Black
- **5 frame colors** - Choose the color that's most visible on your screen
- **5 languages** - EN, US (inch), TR, DE, ES with auto-detection
- **US/inch support** - Generates inch-based prompts for US users
- **Auto-generated Claude prompt** - One click to copy, paste into Claude Code
- **Single HTML file** - Zero dependencies, works offline

## Use as Claude Code Skill

Clone this repo and use it as a Claude Code skill:

```bash
git clone https://github.com/umitkosa/screen-real-size.git
```

Then invoke with `/real-size` in Claude Code.

## Example Output

After calibration, the tool generates a prompt like:

> My screen calibration: pixel/mm: 4.5911, mm/pixel: 0.2178, card: 393x248px. From now on, when I give you dimensions in mm or when designing UI for a screen, use this pixel/mm ratio to calculate real sizes on my display. For example 10mm = 46px on my screen.

Paste this into any Claude Code conversation and it will understand your screen's physical dimensions.

## Why Credit Card?

Credit cards follow the **ISO/IEC 7810 ID-1** standard worldwide:
- Width: **85.6mm**
- Height: **53.98mm**
- Same in USA, Europe, Asia - everywhere

Everyone has one, and the dimensions are guaranteed to be accurate.

## Technical Details

- Pure HTML/CSS/JS - single file, no build step
- Aspect ratio: 85.6 / 53.98 = 1.5857:1
- Frame border compensation: 6px total (2px border + 1px inset per side)
- Typical pixel/mm values: 3.0 - 6.0 (96 DPI = 3.78, 120 DPI = 4.72, 144 DPI = 5.67)

## Author

Prepared by **Umit KOSA** - [@umitkosa](https://github.com/umitkosa)

## License

MIT
