# FOLIO
A compact graphical generative rhythm organism for Linux.  Folio does **not** need a seed sample. It can synthesize its own pulse, noise, resonator, FM and particle percussion. An optional WAV/AIFF/FLAC/OGG seed can also be loaded; Folio extracts short transient-like fragments and treats them as additional generative material.

Keep Folio an **instrument**, not a miniature DAW.

## Controls

- **DENSITY** — probability / activity of rhythmic events.
- **DISORDER** — timing instability and occasional larger clock fractures.
- **MEMORY** — encourages recent rhythmic and timbral behavior to recur.
- **MUTATION** — amount of event-level variation and descendant change.
- **FRAGMENT** — how strongly loaded seed fragments enter the organism.
- **TIMBRE** — shifts the character of the internal synthesis engines.
- **BPM** — central tempo reference for Folio's four interacting clocks.
- **REGENERATE** — creates a new organism.
- **MUTATE** — creates a related descendant of the current organism.
- **LOAD SEED** — analyzes an audio file and extracts usable fragments.
- **SOURCE** — toggles between internal-only and seed-assisted generation.
- **SAVE** — writes the most recent 16 seconds of Folio's actual output to a
  24-bit WAV in `~/Folio_Captures/`.

The important detail about SAVE is that Folio does **not** re-render the
pattern. It saves the audio already held in its rolling memory, so the file is
the strange rhythm you actually heard.

## Architecture

Folio v0.1 is deliberately Python-only. C++ is reserved for DSP that profiling
later proves genuinely needs acceleration. The current architecture is small:

```text
GUI
 |
Genome / controls
 |
Four-clock event ecology
 |             \
Internal DSP    Seed fragment engine
 \             /
   Stereo mixer
       |
 rolling SAVE memory
       |
   audio output

   
# This program is free software: released under the GNU General Public
# License v3.0 or later.
