---
description: Create your first video in 5 minutes using the command line and Curl
---

# Hello World \(Curl\)

This Hello World guide should help to provide a basic understanding of how quick and easy it is to create a simpe video using styled text, a soundtrack and a simple fade transition.

Before you begin ensure you have registered and received your API Keys:

{% page-ref page="request-api-keys.md" %}

### Requirements

This tutorial uses Curl to create your first 'Hello World' video. Curl is a cross platform command line utility that can be used to POST data to an API. Curl is included by default on most modern operating systems including Windows 10, Linux and OS X.

To check if Curl is installed on your operating system open your terminal on Linux/OS X or the Command Prompt in Windows then type:

```
curl --version
```

You should see an output like:

```text
curl 7.55.1 (Windows) libcurl/7.55.1 WinSSL
Release-Date: [unreleased]
Protocols: dict file ftp ftps http https imap imaps pop3 pop3s smtp smtps telnet tftp
Features: AsynchDNS IPv6 Largefile SSPI Kerberos SPNEGO NTLM SSL
```

### Create the Hello World Edit

We'll use a text file to define the JSON data so that it is easy to edit and format. Open your preferred text editor and copy and paste the following JSON, save the file as **hello.json**:

```javascript
{
   "timeline":{
      "soundtrack":{
         "src":"https://s3-ap-southeast-2.amazonaws.com/shotstack-assets/private/dubstep.mp3",
         "effect":"fadeOut"
      },
      "background":"#000000",
      "tracks":[
         {
            "clips":[
               {
                  "type":"title",
                  "src":"Hello World",
                  "start":0,
                  "in":0,
                  "out":5,
                  "transition":{
                     "in":"fade",
                     "out":"fade"
                  },
                  "options":{
                     "style":"minimal"
                  }
               }
            ]
         },
      ]
   },
   "output":{
      "format":"mp4",
      "resolution":"sd"
   }
}
```

### POST the edit to the Shotstack API

You can now go ahead and POST the **hello.json** edit data to the API for rendering, to do this we'll use the _render_ endpoint \(using the staging sandbox URL\). From the same directory as the **hello.json** file run the following Curl command:

```bash
curl -X POST \
     -H "Content-Type: application/json" \
     -H "x-api-key: ptmpOiyKgGYMnnONwvXH7FHzDGOazrIjaEDUS7Cf" \
     -d @hello.json \
     https://api.shotstack.io/stage/render
```

{% hint style="info" %}
Replace the **x-api-key** value with your own sandbox API key.
{% endhint %}

You should receive a 201 response code and payload similar to:

```javascript
{
   "success":true,
   "message":"Created",
   "response":{
      "message":"Render Successfully Queued",
      "id":"d2b46ed6-998a-4d6b-9d91-b8cf0193a655"
   }
}
```

{% hint style="info" %}
Take a note of the **id**, it will be different from the example above, you will need this in the next step.
{% endhint %}

### Poll the API to Check the Render Status

Your video is now either waiting in a queue to be rendered or is being processed. To check the status and know when rendering is complete and the video file is ready we need to poll the API.

Using the id noted in the previous step and your own key, call the staging API using the following command:

```bash
curl -X GET \
     -H "Content-Type: application/json" \
     -H "x-api-key: ptmpOiyKgGYMnnONwvXH7FHzDGOazrIjaEDUS7Cf" \
     https://api.shotstack.io/stage/render/d2b46ed6-998a-4d6b-9d91-b8cf0193a655
```

{% hint style="info" %}
Replace the UUID at the end of the render URL with the **id** output in the previous step.
{% endhint %}

In less than one minute you should receive a 200 response code and payload similar to the output below. The status parameter tells you what stage the render is at, **done** means the video is ready for download. Other status are queued, fetching, rendering, saving and failed.

```javascript
{
   "success":true,
   "message":"OK",
   "response":{
      "id":"d2b46ed6-998a-4d6b-9d91-b8cf0193a655",
      "owner":"zysxdnk0f1",
      "plan":"sandbox",
      "status":"done",
      "data":{
         "output":{
            ...
         },
         "timeline":{
            ...
         }
      },
      "created":"2019-04-16T12:02:42.148Z",
      "updated":"2019-04-16T12:02:51.867Z"
   }
}
```

{% hint style="info" %}
Take note of the **owner** value in the response and also the **id** which will be used when constructing the video download URL.
{% endhint %}

{% hint style="danger" %}
If the status is **failed** then there has been an error and the render will not continue. You can try again or contact us for support.
{% endhint %}

### View or Download the Video File

When the status returned from polling is **done** then the video is ready for download. Videos are stored online for a 24 hour period at the following locations:

| Staging | Production |
| :--- | :--- |
| https://s3-ap-southeast-2.amazonaws.com/shotstack-api-stage-output/ | https://s3-ap-southeast-2.amazonaws.com/shotstack-api-v1-output/ |

To construct a complete download URL you need to combine the storage URL above with your **owner** id \(returned in the polling response\) and the UUID **id** of the original render response plus the file extension \(.mp4\).

The final download URL in our example will look like:

```text
https://s3-ap-southeast-2.amazonaws.com/shotstack-api-stage-output/hwxmtow4o5/d2b46ed6-998a-4d6b-9d91-b8cf0193a655.mp4
```

You can go ahead and open this URL in a modern browser and it will play the video file or you can download it and use it in any way you choose.

{% hint style="warning" %}
Videos are only stored temporarily for 24 hours, rate limits will apply if too many requests to stream or download the file are attempted.
{% endhint %}

### Conclusion

Hopefully you will now have a basic understanding of the key steps needed to create a simple edit:

1. Prepare the edit data
2. POST the edit data to the API
3. Poll the API and wait for the render to complete
4. Download the video

