# Licences and attribution

Stockastic is a single HTML file that runs entirely in the browser. No image data
is uploaded anywhere. It bundles three third-party components and builds on the
published work of several people; this file records the terms for each.

If you redistribute Stockastic — including simply hosting it — the LGPL
obligations for LibRaw apply to you as well. See **LibRaw** below.

---

## Bundled in the page

### LibRaw — LGPL-2.1

Camera RAW decoding. Compiled to WebAssembly and embedded in the page as
base64 via [libraw-wasm](https://github.com/ybouane/LibRaw-Wasm).

- Upstream: <https://www.libraw.org/> · <https://github.com/LibRaw/LibRaw>
- WASM build: <https://github.com/ybouane/LibRaw-Wasm>
- Licence: LGPL-2.1 (LibRaw is dual-licensed LGPL-2.1 / CDDL-1.0; it is used
  here under the LGPL)

**What the LGPL requires of you if you redistribute this file.** LibRaw is a
library, and Stockastic links against it. Because the binary is embedded rather
than linked at runtime, the practical obligations are:

1. State that LibRaw is included and that it is LGPL-2.1 licensed — the page
   footer does this, and so does this file.
2. Provide the complete source of the LibRaw version used, or a written offer
   for it. Linking to the upstream repository above is the normal way to satisfy
   this; if you modified LibRaw, you must publish your modified source.
3. Do not add restrictions that prevent a user from replacing the LibRaw
   component with their own version.

The LGPL does **not** require you to open-source the rest of Stockastic.

Full text: <https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html>

### pako — MIT AND Zlib

Zlib inflate, used to read compressed OpenEXR files. The inflate-only build
(~21 KB) is inlined, since the app never deflates with it.

- Upstream: <https://github.com/nodeca/pako>
- Licence: MIT AND Zlib
- Copyright © 2014–2017 Vitaly Puzrin and Andrei Tuputcyn

### Jost — SIL Open Font License 1.1

Interface typeface. Five latin-subset woff2 faces (300/400/500/600 and 400
italic) are inlined as base64.

- Upstream: <https://github.com/indestructible-type/Jost>
- Licence: SIL OFL 1.1
- Copyright © 2020 Owen Earl, indestructible type\*

The OFL permits bundling and redistribution. It requires that the font not be
sold on its own and that any modified version not use the reserved name.

Full text: <https://openfontlicense.org/>

---

## Methods and prior work

These are not bundled code. They are published approaches that Stockastic
implements, and the people who worked them out deserve the credit.

### Troy Sobotka — AgX, SB2383

The whole picture-formation approach — forming a picture through a mechanism
rather than correcting a measurement, and specifically the inset/outset
structure around a per-channel curve — follows Troy Sobotka's AgX and SB2383
work.

- <https://github.com/sobotka/SB2383-Configuration-Generation>
- <https://github.com/sobotka/AgX>

### Eary Chow — AgX for Blender

The per-channel hue handling, and the structure of the LUT generation used as a
reference while building this, follow Eary Chow's AgX implementation (the one
shipped in Blender).

- <https://github.com/EaryChow/AgX_LUT_Gen>

### Jed Smith — gamut compression

The gamut compression is Jed Smith's algorithm, which became the ACES reference
gamut compress. Distances from the achromatic axis below a threshold are left
untouched; beyond it a power curve asymptotes to a per-channel limit.

- <https://github.com/jedypod/gamut-compress>
- ACES Gamut Compress: <https://github.com/ampas/aces-dev>

### Juan Pablo Zambrano — DCTL implementation

Stockastic's gamut compression was implemented from Juan Pablo Zambrano's DCTL
port, which was the clearest reference for the parameterisation.

- <https://github.com/JuanPabloZambrano/DCTL>

### Saulala

The vibrancy control's behaviour was informed by the Saulala tool.

- <https://www.saulala.com/>

---

## Derived here

For clarity about what is *not* borrowed: the film response curve (an erf arising
from binary grains with log-normally distributed thresholds), the grain model
(binomial statistics over a grain count derived from format and ISO), halation
(a squared-Lorentzian point spread derived from Lambertian diffusion reflecting
off the film base), and the sharpness model (Lorentzian scatter plus an
adjacency effect, applied in density) were derived from the physics for this
project rather than ported from another implementation.

---

\* Verify the copyright holder and year against the upstream repository before
publishing — this file records it from the font's distribution metadata and the
attribution line should match whatever the current release states.
