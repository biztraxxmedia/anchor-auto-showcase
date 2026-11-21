# Anchor Auto Sales Showcase

Live page: https://biztraxxmedia.github.io/anchor-auto-showcase/

A lightweight GitHub Pages site for Anchor Auto Sales (Russell Springs, KY): the holiday media pack plus finished commercials and radio spots.

The page is a single `index.html` plus an `assets/` folder. Labels, contact info, holidays, commercials, and audio are all data objects near the top of the script in `index.html`, so the same layout can be copied and relabeled for another lot.

## Add a holiday video

Holiday slots already exist for New Year, Memorial Day, Fourth of July, Labor Day, Thanksgiving, Black Friday, and Christmas, and all seven already have videos. To replace one, or to add a video on a copied page:

1. Put an H.264 MP4 in `assets/videos/`. Keep it under 50 MB (100 MB is the hard GitHub limit). 1080×1920, 30 fps, AAC audio, and `faststart` work best:

   ```bash
   ffmpeg -nostdin -i source.mov \
     -c:v libx264 -pix_fmt yuv420p -crf 23 -r 30 \
     -c:a aac -b:a 160k -movflags +faststart \
     assets/videos/holiday-thanksgiving.mp4
   ```

2. Make a poster still:

   ```bash
   ffmpeg -nostdin -ss 8 -i assets/videos/holiday-thanksgiving.mp4 \
     -frames:v 1 -q:v 4 assets/posters/holiday-thanksgiving.jpg
   ```

3. In `index.html`, find that holiday in the `HOLIDAYS` array and set the `video` and `poster` fields (this is the line to edit):

   ```js
   video: "assets/videos/holiday-thanksgiving.mp4",
   poster: "assets/posters/holiday-thanksgiving.jpg",
   ```

   Leave `audio` as-is if you still want the song available; the page hides the audio player once a video is present.

## Add a commercial or a radio spot

1. Put the file in `assets/videos/` (mp4, same encoding notes as above) or `assets/audio/` (mp3).
2. For a video, add a poster under `assets/posters/`.
3. Push a new object onto the `COMMERCIALS` or `AUDIO` array in `index.html`. Copy an existing entry and change `id`, `title`, `duration`, `src`, `poster`, and `ratio`.

`ratio` should match the picture: `"16 / 9"` for landscape, `"9 / 16"` for vertical, `"4 / 5"` for the 4×5 spots.
