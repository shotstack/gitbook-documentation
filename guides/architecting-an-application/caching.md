---
description: >-
  Caching assets and source footage to speed up render times and reduce
  bandwidth
---

# Caching

When you perform a render, any source footage, images and audio files are provided by you as URL's which are downloaded and cached on our servers for 24 hours. By cacheing the files we reduce the bandwidth charges you may incur and speed up subsequent renders which rely on the same file. Caching is particularly useful for common assets that are used in multiple renders, for exampl logos, soundtracks and intro/outro videos.

Caching is enabled by default and you do not need to do anything. If you wish to disable caching you can pass a boolean parameter with the timeline settings:

```text
{
   "timeline":{
      "cache": "false",
      ...
   }
}
```

Disabling caching will download all files required by the render. At this time it is not possible to selectively cache files.

