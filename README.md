# VIDU REST API v1

### Introduction

[Vidu](https://www.vidu.io/) allows sales teams to use personalized [videos](https://www.vidu.io/video) / [memes](https://www.vidu.io/memes) / [personal gifs](https://www.vidu.io/personal-gifs) in their sales outreach.

This REST API allows you to automatically generate personalized [videos](https://www.vidu.io/video) / [memes](https://www.vidu.io/memes) / [personal gifs](https://www.vidu.io/personal-gifs). You can also use our Zapier and Make integrations, both of which use this API.

### Authentication

This API uses API Keys to authenticate requests. If you're enrolled in the API beta, you can access your API keys at `Settings > API > API Keys`.

Include an `Authorization` header in your requests as follows:

`Authorization: Bearer {token}`

## Resources

### Me

`GET https://www.vidu.io/api/v1/me`

Returns information about the `User` and `Workspace` associated with the API Key.

```bash
curl -X GET "https://www.vidu.io/api/v1/me" -H "Authorization: Bearer {token}"
```

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

Jobs are usually proccessed within 60 seconds of creation. You can check the progress of a job with the the following endpoint:

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
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/poster.mp4"
      },
      "thumbnail": { // a short looping GIF that's displayed in email and LinkedIn chats
        "extension": ".gif",
        "file_size": 220768,
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/thumbnail.gif"
      },
      "video": { // the full video that plays on the video watch page
        "extension": ".mp4",
        "file_size": 1155204,
        "url": "https://files.vidu.io/2023/9/21/uwgqrasxh/bzMbzRxFUoSd/video.mp4"
      }
    }
  },
  "view_key": "bzMbzRxFUoSd",
  "view_url": "https://videos.yourdomain.com/watch/bzMbzRxFUoSd", // the video can be watched here. append `?analytics=false` to disable open/view analytics
  "view_html": "<a href='https://videos.yourdomain.com/watch/bzMbzRxFUoSd' rel='noopener noreferrer' target='_blank'><img src='https://videos.yourdomain.com/i/bzMbzRxFUoSd.thumbnail.gif' width='496' height='279' alt='Watch the video I made for you' style='border: 1px solid #aaa;'></a><br><a href='https://videos.yourdomain.com/watch/bzMbzRxFUoSd' rel='noopener noreferrer' target='_blank'>Watch the video I made for you</a>", // html that can be used in an email.
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

##### Using in an email

The `job.view_html` allows you to include the personalized asset in an email. You can store this html in your CRM as a custom field and use in an email template.

If you'd like to host the video on your own domain, you can [setup a custom domain](https://intercom.help/viduhq/en/articles/8827055-adding-a-custom-domain).

<img width="607" alt="vidu-email-preview" src="https://github.com/viduhq/api-docs/assets/2526/cfab42e1-0f82-45f4-aa59-04447db56075">
