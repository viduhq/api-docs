# VIDU REST API v1

### Introduction

[Vidu](https://www.vidu.io/) allows sales teams to use personalized [videos](https://www.vidu.io/video) / [meme](https://www.vidu.io/memes) / [personal gif](https://www.vidu.io/personal-gifs) in their sales outreach.

### Authentication

This API uses API Keys to authenticate requests. If you're enrolled in the API beta, you can access your API keys at `Settings > API > API Keys`.

Include an `Authorization` header in your requests as follows:

`Authorization: Bearer {token}`

## Resources

### Me

`GET https://www.vidu.io/api/v1/me`

Returns information about the `User` and `Workspace` associated with the API Key.

```javascript
// RESPONSE
{
  "type": "me",
  "user": {
    "id": 1,
    "type": "user",
    "email": "gavin@vidu.io"
  },
  "workspace": {
    "id": 2,
    "name": "Gavin's Workspace",
    "type": "workspace",
    "identifier": "uwgqrasxh"
  }
}
```

### Jobs

##### `POST https://www.vidu.io/api/v1/jobs`

Enqueues a personalized [video](https://www.vidu.io/video) / [meme](https://www.vidu.io/memes) / [personal gif](https://www.vidu.io/personal-gifs) job.  

```javascript
// POST https://www.vidu.io/api/v1/jobs

{
  "project_id": 26896,
  "inputs": {
    "website_1_url": "www.linkedin.com/in/gavinjoyce",
    "website_2_url": "www.vidu.io"
  }
}
```

```javascript
// RESPONSE
{
  "id": 7654321,
  "type": "job",
  "status": "queued", // "queued" | "processing" | "error" | "complete"
  "inputs": {
    "website_1_url": "www.linkedin.com/in/gavinjoyce",
    "website_2_url": "www.vidu.io"
  },
  "outputs": null,
  "view_key": "bzMbzRxFUoSd",
  "view_url": "https://watch.vidu.io/watch/bzMbzRxFUoSd", // the video can be watched here. append `?analytics=false` to disable open/view analytics
  "project": {
    "id": 26896,
    "name": "REST API Sample Video Recording",
    "type": "project",
    "project_type": "video"
  },
  "inserted_at": "2023-09-21T13:06:58.631391Z",
  "completed_at": null,
}
```

#### `GET https://www.vidu.io/api/v1/jobs/[id]`

Retreives a personalized [video](https://www.vidu.io/video) / [meme](https://www.vidu.io/memes) / [personal gif](https://www.vidu.io/personal-gifs) job.  

```javascript
// GET https://www.vidu.io/api/v1/jobs/7654321

{
  "id": 7654321,
  "type": "job",
  "status": "complete", // "queued" | "processing" | "error" | "complete"
  "inputs": {
    "website_1_url": "www.linkedin.com/in/gavinjoyce",
    "website_2_url": "www.vidu.io"
  },
  "outputs": {
    "assets": {
      "poster": { // a 2 second looping video that auto-plays on the video watch page
        "extension": ".mp4",
        "file_size": 202186,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/poster.mp4"
      },
      "thumbnail": { // a short looping GIF that's displayed in email and LinkedIn chats
        "extension": ".gif",
        "file_size": 220768,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/thumbnail.gif"
      },
      "video": { // the full video that plays on the video watch page
        "extension": ".mp4",
        "file_size": 1155204,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/video.mp4"
      }
    }
  },
  "view_key": "bzMbzRxFUoSd",
  "view_url": "https://watch.vidu.io/watch/bzMbzRxFUoSd", // the video can be watched here. append `?analytics=false` to disable open/view analytics
  "project": {
    "id": 26896,
    "name": "REST API Sample Video Recording",
    "type": "project",
    "project_type": "video"
  },
  "inserted_at": "2023-09-21T13:06:58.631391Z",
  "completed_at": "2023-09-21T13:07:22.199026Z"
}
```

##### Using `job.view_key` in an email

The `job.view_key` allows you to dynamically construct URLs to relevant personalized assets generated in a job.

For example, the following dynamic HTML allows you to embed a personalized video in an email with a `view_key` value (assuming that it's stored in a custom variable called `vidu_introduction_video_view_key` in your outreach tool / CRM in this case):

```html
<p>
  <a href="https://watch.vidu.io/watch/{{vidu_introduction_video_view_key}}" rel="noopener noreferrer" target="_blank">
    <img src="https://watch.vidu.io/i/{{vidu_introduction_video_view_key}}.thumbnail.gif" alt="Watch the video I made for you" style="border: 1px solid #aaa;">
  </a>
  <br>
  <a href="https://watch.vidu.io/watch/{{vidu_introduction_video_view_key}}" rel="noopener noreferrer" target="_blank">Watch the video I made for you</a>
</p>
<br>
```

<img width="607" alt="vidu-email-preview" src="https://github.com/viduhq/api-docs/assets/2526/cfab42e1-0f82-45f4-aa59-04447db56075">


## Webhooks

Webhooks are coming soon and will allow you to subscribe to Vidu events such as:

 * `job.created`
 * `job.completed`
 * `video.opened`
 * `video.viewed`
 * `video.cta_clicked`


