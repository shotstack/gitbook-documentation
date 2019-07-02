---
description: Guidelines on how to create an application incorporating the Shotstack API.
---

# Architecting an Application

Shotstack provides the framework to automate the editing process for your videos and the heavy lifting of rendering hundreds or even thousands of videos concurrently.

Shotstack is useful is in building video based applications and automating workflows where a template can be used and videos created in batches or large volumes.

Shotstack is not really useful by itself although you can quickly create videos using an application like [Postman](https://www.getpostman.com/) and manually editing JSON files.

In order to integrate the Shotstack API in to your application you will need be or hire a developer.

You will also need to already have an existing application or use a developer to build the application and interface to make the service usable by non-technical end users.

## Key steps to build an Application

### **Prepare JSON using SDK**

An edit in Shotstack is defined using JSON which specifies when different assets \(images, videos, titles\) will appear and play on a timeline. In order to create a video you first need to prepare the JSON data so that it contains the correct assets arranged on the timeline.

It is most likely that you would use our SDK to help create this JSON data or you could parse a pre-made JSON template file and replace assets and titles as needed.

Your application might be a form or web based interface for selecting assets or you might use an AI algorithm that determines the best footage. Data and assets could be pulled from databases, CSV files, social network, S3 bucket or stock library API.

{% hint style="info" %}
Think of the JSON edits as templates that can be reused with assets swapped in and modified to create multiple variations of a video.
{% endhint %}

### **Post JSON to API render endpoint**

Once your have prepared an edit using our SDK or directly edited a JSON template you POST the data to the _**render**_ endpoint of our API.

If you are using our SDK this will take care of the request for you. If you are not using an SDK you would use something like Curl or a general purpose API client. You will just need to know the correct URL to use and include your API key in the request headers.

### **Poll render endpoint**

The render process takes some time to complete, a one minute video might take one to two minutes to complete.

Your application needs to poll the API on a regular basis to check the status of the video render by calling the _**render**_ endpoint with the **id** of the current task. When the status is `done` you can proceed to downloading or transferring the video to your application.

If the status is `failed` then you would need to show an error to your users, you may wish to render again or investigate the error.

Anything else you will probably want to inform the user to wait and poll again in  5-10 seconds time.

{% hint style="info" %}
We plan on adding web-hooks shortly which will allow some types of applications to avoid polling and instead be notified when the render is complete.
{% endhint %}

### **Download video when rendered**

Once the video is complete you can fetch it from our servers \(S3\) and transfer it to your own application for further processing.

You may wish to transfer the video to your own S3 or storage service, upload it YouTube, Vimeo or a company like [Mux](https://www.mux.com/) or [Brightcove](https://www.brightcove.com) using their API or a social network like Facebook.

{% hint style="danger" %}
We will store the video on our servers for 24 hours only. After that time they will be deleted. We do not currently provide a video hosting service.
{% endhint %}

