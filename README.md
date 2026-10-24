# Kepler Harmony v0.7.1 (experimental)

This is a **separate VST3 plugin** with a unique product name, plug-in code and bundle identifier. It preserves the Kepler tuning behaviour from the previous source package while allowing independent installation alongside Harmony of the Spheres and Jovian Harmony. This package has **not** been compiled or tested in REAPER.

## Setup

1. Unzip and upload the **contents** of `KeplerHarmony_Independent_v071/` into your separate **Kepler-Harmony** repository, preserving `.github/workflows/build.yml` and `Assets/interplanetary_logo.jpg`.
2. Commit. In **Actions**, check that macOS and Windows builds finish successfully.
3. Download build artifacts, install the VST3, rescan in REAPER.
4. Put this before a Roland plugin if you want to drive it by MIDI. Play and hold a MIDI note; it sets Earth pitch. Set independent channels for the eight planets.
5. Select **Kepler harmony** in the tuning menu. Try `A minor pentatonic`, Harmonic pull `0.85`, Angular-speed glide `0.35`, Earth-year duration `20 seconds`. Disable **4 beats per orbit** for sustained chords.
6. Enable **Microtonal pitch bend** for external instruments. Ensure the receiving Roland plugin responds to pitch bend and is configured to +/-2 semitones. Reserve a distinct MIDI channel per planet for independent bends.

## Scientific versus artistic

- Real (approximate modern) **sidereal orbital periods** and **eccentricities** determine orbital motion; the animation solves Kepler's equation.
- In Kepler Harmony mode, octave-folded `1/T` frequencies become initial reference pitches. A musical palette pulls them towards pitch classes relative to Earth, and the output uses 24-tone (50-cent) pitch-grid candidates.
- **Harmonic pull** blends between the initial orbital-ratio pitch and the selected musical palette. This is deliberate creative retuning, **not a claim that the physical orbits shifted**.
- **Angular-speed glide** multiplies the tuned frequency by the angular-speed ratio due to an elliptical orbit, scaled by the glide depth. Kepler's own proposed 'voices' were based on varying angular speeds between aphelion and perihelion; he did not use the modern transposed `1/T` method as an audio oscillator.
- With nonzero Kepler glide, pitches move continuously *between* quarter tones; the **base tuning** is quarter-tone oriented, but instantaneous pitch is not locked to a 50-cent grid.
- The MIDI pitch-wheel stream is block-rate (when bend on) and uses an assumed +/-2 semitone range. In very fast simulation or complex host routing it may not play ideally. Default pitch bend is off.
- The bundled octave folding and harmonic palettes are deliberately different from Kepler's historical six-planet scale, and also include Uranus and Neptune, unknown in 1619.

## Historical reference

Johannes Kepler, *Harmonices Mundi* (1619), Book V. Helpful contextual source: Physics Today, 'Johannes Kepler’s pursuit of harmony': https://physicstoday.aip.org/features/johannes-keplers-pursuit-of-harmony

## Important limitation

The UI labels/controls and source have been assembled and checked structurally, **but they have not been built or listening-tested**. If a build fails, send the first compilation error line and context.

## Plugin identity (unique)

- JUCE target: `KeplerHarmony`
- Product name and `getName()`: `Kepler Harmony`
- Bundle ID: `com.interplanetarymatt.keplerharmony`
- Manufacturer: `InMt` (shared with your other plugins)
- Plugin code: `KeHm` (distinct from original `HoSp` and Jovian `JoHm`)
- GitHub artifacts: `kepler-harmony-windows`, `kepler-harmony-macos`

This project should be built in a clean GitHub checkout or with a fresh local build folder. Old JUCE VST3 identifiers may still be cached by the DAW; rescan plugins if required.
