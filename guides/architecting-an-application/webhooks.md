---
description: >-
  Receive callback POST notifications whenever the status of a render completes
  or fails
---

# Webhooks

### What is a webhook?

A webhook is a technique used by API's, SaaS providers and online services that send data to a users web server or API endpoints. It is normally used to notify a customer about a change in status or trigger an event from one system to another. The Shotstack webhook will notify your application when a render has finished successfully or failed to complete.

The alternative to a webhook is polling. With polling an application will usually retrieve data from an API endpoint at regular scheduled intervals and process the response. Polling will continue until the expected response is received. With Shotstack you might poll the render endpoint every 5 seconds until the response confirms rendering is complete or failed.

### Why you should use webhooks

Because video rendering can take a relatively long time to complete, potentially several seconds or even several minutes, and because the rendering time for each video may vary in length, polling can be inefficient requiring several unnecessary calls to our API while you wait for the rendering to complete.

Also if you are rendering multiple videos in parallel and polling for several video at a time you can use up your allocated request limits and requests may be throttled by the API.

Instead of polling you can set up a webhook callback using a URL pointing to your server or application that will receive notifications when the render completes. This requires a single request from our API to your application instead of multiple requests from your application to our API.

### Setting up the callback via the Shotstack API

Setting up a webhook callback using the Shotstack API is easy. When a render completes or fails we will POST data to your web server, in the same way that you might post data from an online form or AJAX request from a web site.

Simply provide the URL of the page or endpoint in your application that will receive the POSTed data using the `callback` parameter of an edit. Add the callback parameter as shown below:

```text
{
    "timeline": {...},
    "output": {...},
    "callback": "https://my-application.com/status.php"
}
```

In the example above the callback parameter will POST data to _https://my-application.com/status.php_, where _https://my-application.com/_ is your website or application and _status.php_ is a script that will handle the POSTed request.

The `callback` parameter is also documented in our [API Reference](https://shotstack.io/docs/api/index.html#tocsedit).

### Receiving the callback POST in your application

In the example above we added a callback parameter with a value of _https://my-application.com/status.php_. Assuming your web site or application is hosted at _https://my-application.com_ you would add a _status.php_ script \(or equivalent language\) like: 

```text
<?php
$content = json_decode(file_get_contents("php://input"));
echo $content->status;
```

This PHP script will read the JSON request and output the status of the video.

In a real world application you may want to confirm the status is done and then perform another action such as saving data to a database or downloading the video to your hosting provider.

The data sent to the callback URL is sent as JSON encoded data and the payload looks similar to:

```text
{
    "id": "6d7acbe6-e7c1-4cf8-b8ea-94e7522878cc",
    "owner": "mwipwx4ds3",
    "status": "done",
    "url: "https://shotstack-api-v1-output.s3-ap-southeast-2.amazonaws.com/mwipwx4ds3/6d7acbe6-e7c1-4cf8-b8ea-94e7522878cc.mp4",
    error: null,
    completed: "2020-02-24T11:52:20.810Z"
}
```

While the example above is in PHP you can use any language to receive the JSON and parse or decode it.

If the render fails with a status of failed then an error reason will be provided against the `error` parameter.

### Retries

If the callback POST receives an error code outside the range of 200-399 or a response is not returned by your application within 10 seconds we will cancel the request and retry.

An exponential back-off is used to avoid placing a burden on the server receiving the webhook callback. By default we will try to re-queue the message 10 times with a back-off exponent of 3.

The retries will be as follows:

| Attempt | Back-off \(sec\) | Back-off \(min\) | Cumulative \(sec\) | Cumulative \(min\) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | - | - | 0 | 0 |
| 2 | 8 | 0:08 | 8 | 0:08 |
| 3 | 27 | 0:27 | 35 | 0:35 |
| 4 | 64 | 1:04 | 99 | 1:39 |
| 5 | 125 | 2:05 | 224 | 3:44 |
| 6 | 216 | 3:36 | 440 | 7:20 |
| 7 | 343 | 5:43 | 783 | 13:03 |
| 8 | 512 | 8:32 | 1295 | 21:35 |
| 9 | 729 | 12:09 | 2024 | 33:44 |
| 10 | 900 | 15:00 | 2924 | 48:44 |

### Considerations

* Ensure your application responds within 10 seconds. Make sure your architecture offloads long running processes until after you have sent the webhook a response. For example, respond with a 200 response code and then perform video downloads, database updates and email dispatching in a separate process or script.
* If you queue several videos to render at once, ensure your server is ready to handle multiple callback requests at once. In reality these may be spread over a number of seconds but you should ensure your system can handle the spike in requests and that security mechanisms such as a Web Application Firewall \(WAF\) will not blacklist the Shotstack service.
* Your endpoint for receiving webhook callbacks must be publically available over the internet. In theory anyone can post data to this endpoint. We currently not provide signed payloads so if you are concerned about the validity of the data posted you receive, you should make a request to the API using your API key and the render ID and esnure all data matches.

