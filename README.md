# FujiFoundation

A modernized macOS fork of [Atari800MacX](https://github.com/atarimacosx/Atari800MacX), targeting
macOS 13+ (arm64/x86_64) with aggressive adoption of Apple's current frameworks, toolchains,
and hardware.

---

## Standing on Shoulders

This project would not exist without the work of an extraordinary community of developers who
have dedicated decades to preserving and advancing Atari 8-bit emulation. We want to be
explicit about that.

**David Firth** created Atari800 — the emulator at the core of everything here. His original
work in the early 1990s set the foundation for what became one of the most accurate and
comprehensive Atari 8-bit emulators ever written.

**Perry McFarlane** is the author of the macOS port (Atari800MacX) and contributed an
enormous body of work to the Atari800 core itself — cycle-exact ANTIC/GTIA emulation,
sound improvements, hardware expansions, SDL refinements, and much more. This project is
built directly on his macOS port, and his fingerprints are everywhere in the codebase.

**Mark Grebe** wrote the initial Mac OS X support and many of the platform-specific features
that made Atari800MacX a polished, native Mac application — including H: device support,
multiple disk sets, save state improvements, and XEP80 emulation.

**Petr Stehlik** has coordinated the Atari800 project since 1998, maintaining the broader
ecosystem and keeping the project moving forward across platforms and decades.

**Piotr Fusik**, **Tomasz Krasuski**, **Jacek Poplawski**, **Avery Lee** (Altirra), and a
long list of contributors spanning 30+ years have collectively made Atari800 what it is.
See [DOC/CREDITS](atari800-MacOSX/DOC/CREDITS) for the full list — it is worth reading.
These people gave their time freely, and the Atari community is better for it.

We are grateful for all of it.

---

## What FujiFoundation Is

FujiFoundation is a fork of [atarimacosx/Atari800MacX](https://github.com/atarimacosx/Atari800MacX)
with a specific, focused goal: **aggressive modernization for Apple's current architecture
and standards**.

The original codebase accumulated a lot of legacy over the years — Carbon APIs, old NIB
files, manual memory management patterns that predate ARC, an SDL-based renderer that
bypassed Metal entirely. None of that is a criticism; it reflects the reality of maintaining
a long-lived project across many macOS generations. But with Apple Silicon now the primary
target and macOS 13+ as the baseline, there is real headroom to modernize decisively.

Our approach:

- **Metal-native rendering** — the SDL renderer and surface path are gone; frames go
  directly to a MTKView via a Metal pipeline
- **ARC throughout** — manual retain/release removed; the codebase compiles cleanly under
  Automatic Reference Counting
- **Swift/SwiftUI interoperability** — a bridging header and Swift layer enable modern UI
  panels alongside the existing Cocoa interface
- **Current Xcode toolchain** — project file modernized for Xcode 15+, XIBs replacing NIBs,
  `UniformTypeIdentifiers` replacing deprecated type APIs, weak-linked Carbon for the
  remaining keyboard layout calls
- **Notarization-ready** — entitlements, export config, and a build script for full
  Archive → Export → DMG → Notarize → Staple pipeline
- **VBXE emulation** — Video Board XE support derived from Avery Lee's Altirra implementation
  (see [LEGAL.md](LEGAL.md))

See [MODERNIZATION_BLUEPRINT.md](MODERNIZATION_BLUEPRINT.md) for the full phase-by-phase
record of changes from the upstream fork.

---

## Our Intent

The motivation for this work is twofold.

First, we have other projects in development that build on FujiFoundation as a base. The
details of those projects will become more public as they take shape, but the underlying
idea is that a well-maintained, modernized macOS Atari 800 emulator core is a genuinely
useful foundation for other things. FujiFoundation is that foundation — the part we can
keep public, open, and GPL v2, regardless of what gets built on top of it.

Second, we want to give something back. The Atari emulation community has produced
remarkable work with essentially no commercial incentive. The least we can do is keep
FujiFoundation public, actively maintained, and useful to others who might want a modern
macOS Atari 800 emulator codebase to build from. If the modernization work here is useful
upstream or to other forks, all the better.

We plan to actively maintain this fork, track upstream changes from
[atarimacosx/Atari800MacX](https://github.com/atarimacosx/Atari800MacX), and continue
pushing the modernization forward. We are genuinely open to input — if you have ideas about
where this should go, issues you've found, or improvements you want to contribute, we want
to hear from you.

---

## Building

```bash
cd atari800-MacOSX/src/Atari800MacX
DEVELOPER_DIR=/Applications/Xcode.app/Contents/Developer \
  xcodebuild -configuration Development -scheme Atari800MacX
```

**Requirements:** macOS 13+, Xcode 15+, SDL2.framework (bundled in the project directory).

Build configurations: `Development` / `Deployment` / `Default` (not Debug/Release).

---

## Repository Layout

```
atari800-MacOSX/        ← Xcode project, source, XIBs, assets, SDL2.framework
scripts/                ← build and release automation
ExportOptions.plist     ← notarization export config
MODERNIZATION_BLUEPRINT.md ← phase-by-phase modernization history
LEGAL.md                ← third-party attribution (Altirra VBXE, Ultimate 1MB)
LICENSE                 ← GPL v2
```

---

## Upstream

This fork tracks [atarimacosx/Atari800MacX](https://github.com/atarimacosx/Atari800MacX),
which itself tracks the [Atari800](https://atari800.github.io/) core project.

```bash
git remote add upstream https://github.com/atarimacosx/Atari800MacX.git
git fetch upstream
git merge upstream/master
```

---

## License

GPL v2. See [LICENSE](LICENSE) and [LEGAL.md](LEGAL.md).

This project inherits the GPL v2 license of Atari800 and Atari800MacX. Third-party
components (Altirra VBXE, Ultimate 1MB) are also GPL v2 — see [LEGAL.md](LEGAL.md) for
attribution and specifics.
