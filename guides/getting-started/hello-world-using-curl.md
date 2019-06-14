---
description: Create your first video in 5 minutes using the command line and Curl
---

# Hello World \(Curl\)

This Hello World guide should provide you with a basic understanding of how quick and easy it is to create a simple video using styled text, a soundtrack and a simple fade transition.

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
curl 7.64.0 (x86_64-pc-linux-gnu) libcurl/7.64.0 OpenSSL/1.1.1b zlib/1.2.11 libidn2/2.0.5 libpsl/0.20.2 (+libidn2/2.0.5) libssh/0.8.6/openssl/zlib nghttp2/1.36.0 librtmp/2.3
Release-Date: 2019-02-06
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: AsynchDNS IDN IPv6 Largefile GSS-API Kerberos SPNEGO NTLM NTLM_WB SSL libz TLS-SRP HTTP2 UnixSockets HTTPS-proxy PSL
```

### Create the Hello World Edit

We'll use a text file to define the JSON data so that it is easy to edit and format. Open your preferred text editor and copy and paste the following JSON, save the file as **hello.json**:

```javascript
{
   "timeline":{
      "soundtrack":{
         "src":"https://s3-ap-southeast-2.amazonaws.com/shotstack-assets/music/moment.mp3",
         "effect":"fadeOut"
      },
      "background":"#000000",
      "tracks":[
         {
            "clips":[
               {
                  "asset": {
                     "type":"title",
                     "text":"Hello World",
                     "style":"minimal"
                  },
                  "start":0,
                  "length":5,
                  "transition":{
                     "in":"fade",
                     "out":"fade"
                  }
               }
            ]
         }
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

Using the **id** noted in the previous step and your own key, call the staging API using the following command:

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
      "owner":"hckwccw3q3",
      "plan":"sandbox",
      "status":"done",
      "url":"https://s3-ap-southeast-2.amazonaws.com/shotstack-api-stage-output/hckwccw3q3/d2b46ed6-998a-4d6b-9d91-b8cf0193a655.mp4",
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

{% hint style="danger" %}
If the status is **failed** then there has been an error and the render will not continue. You can try again or contact us for support.
{% endhint %}

### View or Download the Video File

When the status returned from polling is **done** then the video is ready for download. Videos are stored online for a 24 hour period at the following locations:

| Staging | Production |
| :--- | :--- |
| https://s3-ap-southeast-2.amazonaws.com/shotstack-api-stage-output/ | https://s3-ap-southeast-2.amazonaws.com/shotstack-api-v1-output/ |

Download the video using the URL returned in the get render status response:

```text
curl -O https://s3-ap-southeast-2.amazonaws.com/shotstack-api-stage-output/hwxmtow4o5/d2b46ed6-998a-4d6b-9d91-b8cf0193a655.mp4
```

{% hint style="warning" %}
Videos are only stored temporarily for 24 hours, rate limits will apply if too many requests to stream or download the file are attempted.
{% endhint %}

### Conclusion

Hopefully you will now have a basic understanding of the key steps needed to create a simple edit:

1. Prepare the edit data
2. POST the edit data to the API
3. Poll the API and wait for the render to complete
4. Download the video

