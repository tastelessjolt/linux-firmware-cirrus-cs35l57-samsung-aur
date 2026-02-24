# Maintainer: Harshith G <drew.jones@goldfishgateway.com>
pkgname=linux-firmware-cirrus-cs35l57-samsung
pkgver=4.7.0
pkgrel=1
pkgdesc="Cirrus Logic CS35L57 firmware for Samsung laptops"
arch=('any')
url="https://semiconductor.samsung.com"
license=('LicenseRef-Samsung-proprietary')
makedepends=('unzip' 'zstd')
source=("BASW-A4285A20_1063.ZIP::https://org.downloadcenter.samsung.com/downloadfile/ContentsFile.aspx?CttFileID=11284027&CDCttType=DR&ModelType=C&ModelName=&VPath=DR/202602/20260209091248829/BASW-A4285A20_1063.ZIP")
sha256sums=('e6a4cb8197923e0eff0545500b0f0f26630faf93f5e7364ac19dc9789a34b4de')
options=('!strip' '!debug')

_firmware_files=(
    b2_dflt_35l56_4.7.0.wmfw
    b2_dflt_ss0_c910_lw_l1u0.bin
    b2_dflt_ss0_c910_rw_l2u1.bin
)

prepare() {
    cd "$srcdir"
    # The ZIP may contain nested archives or directories; extract recursively
    find . -name '*.zip' -o -name '*.ZIP' | while read -r z; do
        unzip -o -d "${z%.*}" "$z" 2>/dev/null || true
    done
}

build() {
    cd "$srcdir"
    for fw in "${_firmware_files[@]}"; do
        local found
        found=$(find . -name "$fw" -print -quit)
        if [[ -z "$found" ]]; then
            echo "ERROR: Could not find $fw in extracted driver" >&2
            return 1
        fi
        zstd --compress --force -o "$fw.zst" "$found"
    done
}

package() {
    cd "$srcdir"

    install -d "$pkgdir/usr/lib/firmware/cirrus/samsung"

    # Install compressed firmware files
    for fw in "${_firmware_files[@]}"; do
        install -Dm644 "$fw.zst" "$pkgdir/usr/lib/firmware/cirrus/samsung/$fw.zst"
    done

    # Install license notice
    install -Dm644 /dev/stdin "$pkgdir/usr/share/licenses/$pkgname/LICENSE" <<'EOF'
The firmware files packaged here are proprietary to Samsung Electronics Co., Ltd.
and/or Cirrus Logic, Inc. They are extracted from the official Samsung Windows
audio driver (BASW-A4285A20_1063). Redistribution may be subject to Samsung's
and/or Cirrus Logic's license terms.
EOF

    # Create symlinks
    cd "$pkgdir/usr/lib/firmware/cirrus"
    ln -s samsung/b2_dflt_35l56_4.7.0.wmfw.zst cs35l57-b2-dsp1-misc-144dc910-l1u0.wmfw.zst
    ln -s samsung/b2_dflt_35l56_4.7.0.wmfw.zst cs35l57-b2-dsp1-misc-144dc910-l2u1.wmfw.zst
    ln -s samsung/b2_dflt_ss0_c910_lw_l1u0.bin.zst cs35l57-b2-dsp1-misc-144dc910-l1u0.bin.zst
    ln -s samsung/b2_dflt_ss0_c910_rw_l2u1.bin.zst cs35l57-b2-dsp1-misc-144dc910-l2u1.bin.zst
}
