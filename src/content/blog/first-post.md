---
title: 'Syncing Features With the Song Track'
description: 'How the metronome, white flash, music start, and obstacle spawning are synchronized to the song track.'
pubDate: 'May 21 2026'
heroImage: '../../assets/blog-placeholder-3.jpg'
---

Feature: syncing something to the rhythm of the music

## Key Point

In `test_shard.py`, sync is manual and timer-based. The code assumes `BPM = 136` matches the song, starts a session timer with `_start_new_session()`, and then fires `_on_beat()` every `60_000 / 136` milliseconds.

The metronome click, white flash, and obstacle spawning are all lined up from that same beat timing.

## Metronome

1. Make a clock for the metronome timing.

This calculates when the next beat should happen. Since `BPM = 136`, one beat is `60_000 / 136` milliseconds.

2. Reset the session so the beat count starts from the beginning.

This is the reset point. It is like starting the song count again at 1 instead of continuing from wherever the old count stopped.

After one beat passes, the timer checks when the next beat should come. When it reaches that time, `_on_beat()` runs again.

## White Flash

1. The timing of one flash is hardcoded to 3 frames, which is about 50ms at 60 FPS.

The flash starts when `trigger()` is called. Then `update()` counts it down over time until the flash disappears.

2. The white overlay is defined here.

So the flash is not a separate image. It is a white transparent layer placed over the screen.

## Lining Up Music, White Flash, and Metronome

Both the metronome and white flash happen through `_on_beat()`. The timing for `_on_beat()` comes from `_get_next_session_beat_ms()`, which acts like the clock for the song.

In the boss battle phase, the song starts inside `_on_beat()` too.

The song itself is not reading the beats. The code is counting the beats manually and assuming that count matches the song.

## Lining Up Obstacle Spawning With the Music

This equation checks where the current beat lands inside the measure. In a 4-beat measure, it is checking the count like this:

It is like tapping along to a regular song. The beat keeps moving forward, and the code uses the remainder to know where it is inside the measure.

That is why the obstacle can spawn on a specific beat instead of appearing randomly. The timer controls the beat, the beat controls `_on_beat()`, and `_on_beat()` controls the metronome, flash, music start, and obstacle spawning.

## Short Version

- `_get_next_session_beat_ms()` decides when the next beat should happen.
- `_on_beat()` runs when that beat time arrives.
- `_on_beat()` triggers the metronome click.
- `_on_beat()` triggers the white flash.
- `_on_beat()` starts the boss music during the boss battle phase.
- `_on_beat()` uses `beat_in_bar` to decide when obstacles spawn.
