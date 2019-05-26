---
description: Learn the basics of how a video edit is put together using JSON
---

# Core Concepts

## Edit videos using code

Shotstack is a cloud based video editing API. Unlike traditional desktop video editing applications like Adobe Premiere or After Effects, Shotstack is purely code based - you create an edit using code. The API uses a REST architectural style using JSON to describe how the video should be edited. A number of SDK's in different languages are available to interface with the API and create the JSON requests.

Although code based, the API follows many of the principles of desktop editing software such as a timeline, tracks and clips. If you have used with Adobe Premiere, After Effects or even Flash some of these concepts should be familiar, all be it without a graphical user interface.

These core concepts and principles are described below:

### Edit

An edit encompasses everything about the video that you want to create and is made of two components - the **timeline** which describes the assets \(videos, images and titles\) that you want use and how they are  arranged \(edited\) and the **output** format \(gif or mp4\) and resolution \(HD, SD, mobile, etc..\).

```javascript
{
    timeline: {...},   // the main video edit description
    output: {...}      // the output format and resolution
}
```

{% hint style="info" %}
edit is the JSON payload that you POST to the _render_ endpoint to create your video.
{% endhint %}

### Timeline

The timeline represents the time that the video will play for, using seconds and starting from 0. A timeline is made up of **tracks** which are like layers that contain clips.

```javascript
{
    timeline: {
        tracks: [{...}]   // array of tracks
    },
    ...
}
```

### Tracks

Tracks are like layers within the timeline which span the entire length of the timeline, a track contains one or more **clips**. Tracks can be visualised as layers that can be placed one on top of another. Clips on the top most track will obscure those on tracks below it. This can be useful for when you want to layer a title over a video clip or you want to fade between clips.

Tracks also help to logically organise different types of content, for example a title track which plays over the top of a video and a watermark track that plays over the top of everything.

Tracks are an array within the timeline, the first element is the top track and the last element is the bottom most track:

```javascript
{
    timeline: {
        tracks: [
            {
                ...   // top track
            },
            {
                ...   // bottom track
            }
        ]
    },
    ...
}
```

### Clips

Clips are where you select the asset \(video, image or title\) you want to display within a track on the timeline, when it starts, how long it plays for and what effects, transitions and filters you want to apply.

Clips are placed on a track at a specific **start** time, for example a clip with a **start** time of 3 will appear in the video after three seconds have played. Clips also have a **length** which determines how long the clip will play for in seconds.

Each **asset** type has a specific set of options and features but you must specify the **type** of asset and also the **content** of the asset such a URL **src** to a video or image file or for titles a **text** string.

```javascript
{
    timeline: {
        tracks: [
            {
                clips: [
                   {
                       // place an image at the very start of the track/timeline that plays for 4 seconds.
                       "asset":{
                           "type": "image",
                           "src": "https://s3-ap-southeast-2.amazonaws.com/my-bucket/photo.jpg",
                       },
                       "start": 0,
                       "length": 4
                    },
                    {
                        // place a video that starts on the fourth second of the track/timeline that has 
                        // the first two seconds (in: 2) trimmed and plays for 4 seconds (out: 6).
                       "asset":{
                           "type": "video",
                           "src": "https://s3-ap-southeast-2.amazonaws.com/my-bucket/footage.mp4",
                           "trim": 2
                       },
                       "start": 4,
                       "length": 6
                    }
                ]
            },
        ]
    },
    ...
}
```

{% hint style="danger" %}
Do not place clips on a track so that their start or end times overlap, this will result in the clips flashing between each other as the API does not know which clip to display first.
{% endhint %}

A clip can also have transitions, effects and filters applied to them. A clip may look something like this when all options are applied:

```javascript
{
  "asset":{
    "type": "video",
    "src": "https://s3-ap-southeast-2.amazonaws.com/my-bucket/footage.mp4",
    "trim": 2,
    "volume": 0.5
  },
  "start": 0,
  "length": 4,
  "transition": {
    "in": "fade",
    "out": "fade"
  },
  "filter": "boost",
  "effect": "slideRight"
}
```

From these basic building blocks you should be able to assemble a sophisticated, reusable template to create videos. Assets can be replaced or clips added using loops, conditions and other coding constructs allowing you to build a range of video based applications.

