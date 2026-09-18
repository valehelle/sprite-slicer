# Sprite Slicer

Cuts an AI-generated sprite sheet into game-ready frames, in the browser.

**[Open it →](https://valehelle.github.io/sprite-slicer/)**

Drop a sheet in and it finds the rows, cuts the frames, lines them up and
plays each row back animated. Nothing is uploaded — it all runs on your
machine, and it works offline once loaded.

## What a sheet needs

- A flat background the creature never uses. Magenta is the convention. The
  colour is read off the corners, so it does not have to be exactly `#FF00FF` —
  a sheet that has been through JPEG comes back as something like `237,3,249`
  and still works.
- Clear gaps between frames and between rows. Frames that touch are found as
  one frame.
- The same number of frames in every row.

Everything else is measured: where the rows sit, where each frame's edges are,
and where the creature's body is so the frames line up instead of shuffling.
When a row cannot be cut it says which one and why.

## What it does to each frame

Keys out the background with a flood fill from the edges, so a pale area
enclosed by the creature survives instead of being punched through. Pulls the
key's colour cast back out, or an orange creature on magenta keeps a violet
rim. Grows the creature's colours outward so a downscale has no background
left nearby to average into a halo. Finds each frame and pins the row on
whichever part of the creature holds stillest. Scales down with a Lanczos
filter, draws a dark rim, and snaps to a small palette.

The reference animation at the top is a real Ragnarok Online sprite run
through the same pipeline, so there is always a known-good loop on screen to
judge a new sheet against.
