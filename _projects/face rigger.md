---
title: "Face Rigger"
date: 2021-08-15 +0000
image: 
  path: /images/face-rigger.png
  thumbnail: /images/face-rigger.png
  caption: "Face Rigger in Action"
---

Face Rigger is a fun project I setup when learning about python facial detection.

It took the positional data of your face and then rendered randomly coloured shapes over top it. This would then either be displayed in a window or sent to a virtual web cam.

Orginally I had problems with the facial recognition being too slow and leading to a choppy framerate. However, I overcame this limitation by making use of a buffered frame so that movement could be be interpolated so that while the facial recognition may only be running at 12FPS, I could have the camera run at 30 with the majority of the frames being interpolated. This didn't solve the problem completely as too much interpolation caused jittery movement, however this was still better than a low framerate.