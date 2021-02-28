---
description: System considerations and limitations
---

# Limitations

### Render Time

Rendering video is a CPU and memory intensive process and takes time to complete – expect 1 to 4 seconds rendering time per second of video.

It will be slower at higher resolutions \(i.e. 1080p HD vs SD\) and with effects, filters and transitions applied. Keep this in mind when doing status requests to check if a render has completed or not.

### Usage Limits

The production API has the following usage limits:

* 25 requests per second \(burst to 50 r/s\)
* 10,000 requests per day \(including polling and renders\)

Limits may be increased if needed, please contact us.

The sandbox API has the following usage limits:

* 10 requests per second
* 2,000 requests per month \(including polling and renders\)

To reduce the number of polling requests consider using [webhooks](webhooks.md).

### Environment Limits

The render environment has the following limits:

* Max 15 minutes render time.
* The amount of footage you can ingest and create for each render is 512MB when using the [local disk type](disk-types.md#speed-optimised-local-disk-type) – i.e. the original footage you send to be trimmed and edited plus the size of the final output video must be less than 512MB.
* When using the [mount disk type](disk-types.md#file-size-optimised-mount-disk-type) you can ingest up to 5GB of source footage and assets and output a rendered video with a file size of 512MB.

