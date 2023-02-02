---
title: "Bad Apple in Excel"
date: 2022-10-12 +0000
image: 
  path: /images/badapple.png
  thumbnail: /images/badapple.png
  caption: "Bad Apple in Excel"
---

A video rendering engine using excel formulas and conditional formatting.

It works by for each cell referencing a lookup in a data sheet and then applying conditional formatting to it. This data sheet is calculated ahead of time and represents the luminance of each pixel in the image.

Additionally, while rendering you can get a weird artifacts when excel is unable to apply the conditional formatting fast enough and instead it's saved to last the last known value for some pixels.

![Weird Video Artifact](/images/badapple-artifact.png)

## Constants

| Name | Description |
| ---- | ------- |
| WIDTH | The width of the video |
| HEIGHT | The width of the video |
| FPS | The framerate of the video |
| START_TIME | The time the first frame of the video should be rendered |

## Formulas

| Name | Formula |
| ---- | ------- |
| CURRENT_FRAME_NUMBER | `=(CURRENT_TIME - START_TIME) * FPS` |
| GET_POS | `=((ROW() - 1) * WIDTH) + COLUMN()` |
| GET_PIXEL | `=ADDRESS(CURRENT_FRAME_NUMBER, GET_POS, 1, 1, "DATA")` |

Real Time Rendered:

<iframe
  width="384"
  height="216"
  src="https://www.youtube.com/embed/XAERR5sjKbs"
  frameborder="0"
  allowfullscreen
></iframe>
