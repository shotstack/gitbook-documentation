---
description: Choose the correct disk type for your render task
---

# Disk Types

Shotstack has two disk types, each of which has specific use cases and are optimised for speed or storage space. If you are not experiencing any issues with file size or running out of disk space then you can use the default and do not need to make a selection, it will be chosen for you.

### Speed Optimised - Local Disk Type

By default, each render uses a **local** disk which is optimised for speed. Source footage and assets are downloaded directly on to the instance that performs the render. This allows many short videos to be rendered in parallel without running in to any read/write or throughput issues.

The maximum file size for the local disk type is **512MB**, which is used for both the source footage and the rendered output. In most instances you should optimise your source footage and output file to use local disk types.

### File Size Optimised - Mount Disk Type

The **mount** disk type is a special type of disk suitable for when your source and output footage exceeds the 512MB limit. You should use this disk type when working with larger files or outputting longer high resolution videos. The mount type allows total source file storage of **5GB** and an output file size of **512MB** or each render.

The mount disk type takes longer to load and is slower than using local disk type so should only be used when required. If you render too many videos in parallel using the mount disk type you may experience read/write or throughput issues.

### Which Type Should I Use?

* Unless you are experiencing out of disk space errors you should use the **local** disk type.
* If you render videos in batches or perform several concurrent render tasks you should optimise your assets and output to complete withing 512Mb using the **local** disk type.
* If you are experiencing disk space errors or you know you will be handling files totaling more than 512Mb or creating long, high resolution \(1080p\) videos try the **mount** disk type.

### Setting the Disk Type

The disk type is set at the root level of each render that you POST to the Shotstack API. The default value is **local** so you do not need to pass any value to use the **local** disk.

If you want to explicitly choose **local** you can use the **disk** parameter:

```text
{
    "timeline": {...},
    "output": {...},
    "disk": "local"
}
```

To use the **mount** disk type set the **disk** parameter to mount:

```text
{
    "timeline": {...},
    "output": {...},
    "disk": "mount"
}
```

