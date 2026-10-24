# Kepler Harmony v0.7.3 — Continuous orbital pitch bend

This update lets a planet's changing **angular speed** drive continuous MIDI pitch bend, rather than only changing the internal oscillator pitch. It keeps the Kepler Harmony identity (KeHm) separate from your other VST3 instruments.

## Start in REAPER

1. Put Kepler Harmony before the Roland instrument(s) in the MIDI FX chain, or route MIDI by channel to separate tracks.
2. Choose **Kepler harmony**, turn on **MIDI output** and **Pitch bend: orbit -> pitch**, and choose **+/- 12 semitones** in the Kepler UI.
3. **Set each receiving Roland synth's pitch-bend range to +/- 12 semitones**. This MUST match the plug-in's setting. If the Roland instrument only supports +/- 2, choose +/- 2 on both, but substantial Mercury motion may clip because the pitch range is inadequate.
4. Assign each planet a different MIDI channel and make sure each receiving synth listens on that channel. Ordinary MIDI 1.0 pitch bend is channel-wide.
5. Set **Kepler angular-speed glide** to 0.4 initially; try 1.0 for the physical (exaggerated-eccentricity-dependent) range. For a faithful eccentricity shape set **Ellipse exaggeration = 1**.
6. Turn **4 beats per orbit** off when evaluating pitch glide, to avoid repeated note gates. Hold a key on your MIDI keyboard.
7. With **1 Earth year = 20 seconds**, Mercury completes an orbit in about 4.8 seconds and sweeps noticeably. Venus will hardly move.

**Science vs creative mapping:** the animated orbit and changing angular speed come from Kepler's equations using approximate planetary orbital periods and eccentricities. The central note is octave-folded and optionally quantised/harmonised artistically; the speed-driven glide bends around that tuned pitch. This is a sonification, not sound emitted by the planets.

**Important limitation:** bend is transmitted at block-rate capped by a 5ms update check (usually much faster than perceptual requirements). Pitch bend is limited by the receiver's configured range; when the chosen +/- 2 range is exceeded, the sound clips at the limit. On a stopped chord, notes are released and wheels return to centre. Very rapid orbit speed and sample-buffer settings can affect event resolution.

## Source build

Upload the updated project files to GitHub, keeping `.github/workflows/build.yml`. Download artifacts from the successful Actions build. This revision has been source-checked but NOT compiled/tested with Roland/REAPER here.


## v0.7.4 Pitch-bend diagnostics

In Kepler harmony mode, with MIDI output and Pitch bend enabled, and four-pulses-per-orbit OFF, hold a MIDI key. The orbital display now shows `MERCURY MIDI PITCH BEND: n / 16383`. This must change with simulated orbital position. Values near 8192 are neutral.

REAPER test: insert Kepler Harmony then **ReaControlMIDI** after it in the same FX chain; enable its MIDI activity log to check `Pitch Wheel` events on Mercury's chosen MIDI channel. The subsequent Roland synth must match the selected +/-12 semitone pitch-bend sensitivity. If the on-screen value changes but the log doesn't, inspect plug-in MIDI output forwarding in REAPER and ensure the VST3 compiled version is refreshed. If the log changes and sound doesn't, inspect the synth's pitch-bend routing.

Version is a source patch, not yet compiled or verified in REAPER.
