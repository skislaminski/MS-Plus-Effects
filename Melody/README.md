# Melody 1.00

![Melody](picture.png)

A generative melody player that plays random notes in a scale and key you choose, or in the key of the note you played last, in the tempo of the patch or at its own.

- **Version:** 1.00
- **Files:** `MELODY.ZD2` and `MELODY.ZIC` (install both)
- **Played by:** the footswitch
- **On the pedal:** PITCH SHIFT, like every effect of this collection (see [About the files](../README.md#about-the-files))
- **Id:** `07000f91`
- **DSP load:** 69, as declared to the pedal (a patch on the MS-60B+ has room for 270)
- **Delay memory:** none
- **Tested on:** one Zoom MS-60B+, firmware 1.20 only (the same effect code, installed in its own category; see [About the files](../README.md#about-the-files))

## What it does

Melody plays a synth line of random notes from a scale, over two octaves, while it is switched on. Seed 1 to 99 gives a melody of 16 notes that repeats, a different one for every number; Seed 0 never repeats. Walk, Rest and Gate set how the line moves, how often it pauses and how long the notes are held. The bass passes unchanged; the melody is added.

## Playing it

- After you insert it, load a patch or change the chain, Melody is silent, even with the LED on. Switch it off and on once. Save the patch with Melody switched off: then one press starts it.
- LED on starts at once with a note (with Seed 1 to 99, the first note of its 16). LED off stops it; the last note fades out in about 30 ms.
- With Root at Bass, play a note, then switch Melody on: that note becomes the key and stays while the melody runs. Play one note at a time for this.
- Leave Tempo on Sync to play in the patch tempo. Div sets quarter notes, eighths, eighth triplets or sixteenths.
- Walk 100 moves in steps of the scale; Walk 0 jumps anywhere in the two octaves. Rest 0 plays every step.

## Knobs

| Knob | Range | Default | What it does |
|---|---|---|---|
| `Scale` | Major to Chrom (10 scales) | Major | The notes it may use: Major, Minor, Penta and PentM (major and minor pentatonic), Blues, Dor (Dorian), Phryg (Phrygian), Whole (whole tone), Harm (harmonic minor), Chrom (all twelve). |
| `Tempo` | 40 to 250 BPM, Sync | Sync | Sync: the tempo of the patch (BPM module, tap). 40 to 250: its own tempo in BPM. |
| `Level` | 0 to 100 | 80 | Level of the melody. The bass is not affected. |
| `Root` | Bass, C to B | Bass | The key. Bass: the note you played last when you switch on, rounded to the nearest semitone. C to B: that note. |
| `Oct` | -1, 0, +1, +2 | +1 | Octave of the lowest note (at 0 the root is between C1 and B1); the melody spans two octaves above it. |
| `Div` | 1/4, 1/8, 1/8T, 1/16 | 1/8 | How often a note is played: every quarter, eighth, eighth triplet or sixteenth of the tempo. |
| `Seed` | 0 to 99 | 1 | 0: a new melody all the time. 1 to 99: a melody of 16 notes that repeats, a different one for every number. |
| `Walk` | 0 to 100 | 60 | How the melody moves: 0 = every note anywhere in the two octaves, 100 = every note one step of the scale from the one before. |
| `Rest` | 0 to 100 | 25 | How often a note is left out, 0 to 90 %. The first note after switching on always plays. |
| `Gate` | 0 to 100 | 55 | How long a note is held, 10 % to 100 % of the step. At 100 the notes run into each other. |
| `Tone` | 0 to 100 | 50 | Brightness: the cutoff of the low-pass and how far every note opens it (an accented note more). |
| `Wave` | Saw, Pulse, Sine, Organ | Saw | Sound of the voice: Saw, Pulse (hollow), Sine (with a sine an octave below), Organ (sine with octave and double octave). |

## Good to know

- With Tempo on Sync, a new patch tempo may only arrive once you move the Tempo knob.
- Below Tone 30 the melody also gets quieter at Oct +1 and +2. At Tone 50 it is equally loud in every octave.
- Inserting or moving an effect in the chain while it plays makes Melody silent again: switch it off and on once.

## Installing

Read the safety notes in the [collection's README](../README.md#read-this-first) and stomphacks' [SAFETY.md](https://github.com/thammer/stomphacks/blob/main/SAFETY.md) first. Install with [stomphacks](https://github.com/thammer/stomphacks), from its folder, one command at a time, checking each result:

1. `.venv/bin/python3 tools-pedal/safe_connect.py session/` connects and confirms that AUTO SAVE is off.
2. `.venv/bin/python3 tools-pedal/backup_pedal.py backup/` backs up the pedal (once per pedal).
3. `.venv/bin/python3 tools-pedal/pedal_diy.py install <this folder>/MELODY.ZD2 --dry-run`, then the same without `--dry-run`. It uploads `MELODY.ZIC` alongside: keep it next to the `.ZD2`, without it pedal_diy.py refuses.
4. `.venv/bin/python3 tools-pedal/readback.py MELODY.ZD2 session/MELODY-back.ZD2` and `cmp <this folder>/MELODY.ZD2 session/MELODY-back.ZD2`: they must be identical.
5. Try it in an unsaved patch, with the amp or headphones turned down.

To update to a newer version: take the effect out of every patch, `pedal_diy.py uninstall <this folder>/MELODY.ZD2` (the new file has the old one's name and id), then install the new one as in step 3 and read it back to a new path (for example `session/MELODY-back2.ZD2`; readback.py does not overwrite a file). The effect appears under PITCH SHIFT on the pedal (see the collection's README).
