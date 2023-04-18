---
title: "Mediaify"
date: 2023-04-15 +0000
image:
  path: /images/mediaify.png
  thumbnail: /images/mediaify.png
  caption: "Medaifiy"
---

Mediaify is a media encoding library for python that aims to provide a declarative interface for re-encoding, available [here](https://pypi.org/project/mediaify/).

I started this project after I realised that most of the OpenBooru modules was so non-domain specific that they could be could be turned into their own libraries. While this wasn't my first python library, it was the first one I developed with any actual merit. The goal was to be able to provide a file to the library and have it be re-encoded without any hassle, even batch encoded. On all accounts I succeeded on this goal and I'm still making improvements to it today.

## Example

```python
import mediaify
from mediaify import (
    ResizeConfig,
    WEBPImageEncodeConfig,
    ImageConfig,
    UnencodedConfig,
)

encoding_config = [
    JPEGEncodeConfig(
        resize=ResizeConfig(
            max_height=64,
            max_width=64,
        ),
        quality=80,
    ),
    PNGEncodeConfig(
        resize=ResizeConfig(
            height=256,
            width=256,
        )
    ),
    WEBPImageEncodeConfig(
        quality=90
    ),
    UnencodedConfig()
]


with open('./landscape.webp', 'rb') as f:
    data = f.read()


mediaify.batch_encode_image(data, encoding_config)
>>> [
    ImageFile(64x33, image/webp, 802.0B),
    ImageFile(256x134, image/png, 78.7KB),
    ImageFile(512x268, image/jpeg, 42.3KB),
    ImageFile(1600x840, image/webp, 284.3KB)
]
```
