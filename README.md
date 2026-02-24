# linux-firmware-cirrus-cs35l57-samsung

AUR package providing Cirrus Logic CS35L57 speaker amplifier firmware for Samsung laptops.

## What this package does

Extracts firmware files from the official Samsung Windows audio driver and installs them for use by the Linux `cs35l57` kernel driver.

### Installed firmware

| File | Path |
|------|------|
| `b2_dflt_35l56_4.7.0.wmfw` | `/usr/lib/firmware/cirrus/samsung/` |
| `b2_dflt_ss0_c910_lw_l1u0.bin` | `/usr/lib/firmware/cirrus/samsung/` |
| `b2_dflt_ss0_c910_rw_l2u1.bin` | `/usr/lib/firmware/cirrus/samsung/` |

### Symlinks created

```
/usr/lib/firmware/cirrus/cs35l57-b2-dsp1-misc-144dc910-l1u0.wmfw.zst -> samsung/b2_dflt_35l56_4.7.0.wmfw.zst
/usr/lib/firmware/cirrus/cs35l57-b2-dsp1-misc-144dc910-l2u1.wmfw.zst -> samsung/b2_dflt_35l56_4.7.0.wmfw.zst
/usr/lib/firmware/cirrus/cs35l57-b2-dsp1-misc-144dc910-l1u0.bin.zst  -> samsung/b2_dflt_ss0_c910_lw_l1u0.bin.zst
/usr/lib/firmware/cirrus/cs35l57-b2-dsp1-misc-144dc910-l2u1.bin.zst  -> samsung/b2_dflt_ss0_c910_rw_l2u1.bin.zst
```

## Installation

```bash
# From AUR
yay -S linux-firmware-cirrus-cs35l57-samsung

# Or manually
git clone https://aur.archlinux.org/linux-firmware-cirrus-cs35l57-samsung.git
cd linux-firmware-cirrus-cs35l57-samsung
makepkg -si
```

## License

The PKGBUILD is licensed under [0BSD](LICENSE). The firmware files themselves are proprietary to Samsung Electronics and/or Cirrus Logic.
