# VIDU REST API v1

### Authentication

The [Vidu](https://www.vidu.io/) REST API uses API Keys to authenticate requests. If you're enrolled in the API beta, you can access your API keys at `Settings > Developers > API Keys`.

Include an `Authorization` header in your requests as follows:

`Authorization: Bearer {token}`

## Resources

### Me

`GET https://www.vidu.io/api/v1/me`

Returns information about the `User` and `Workspace` associated with the API Key.

```javascript
// RESPONSE
{
  "user_id": 98765,
  "workspace_id": 1234567
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
  "view_url": "https://watch.vidu.io/watch/bzMbzRxFUoSd",
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
      "poster": {
        "extension": ".mp4",
        "file_size": 202186,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/cvslemxci/boDeEVGYyWdQ/poster.mp4"
      },
      "thumbnail": {
        "extension": ".gif",
        "file_size": 220768,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/cvslemxci/boDeEVGYyWdQ/thumbnail.gif"
      },
      "video": {
        "extension": ".mp4",
        "file_size": 1155204,
        "type": "image",
        "url": "https://files.vidu.io/2023/9/21/cvslemxci/boDeEVGYyWdQ/video.mp4"
      }
    }
  },
  "view_key": "bzMbzRxFUoSd",
  "view_url": "https://watch.vidu.io/watch/bzMbzRxFUoSd", 
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


