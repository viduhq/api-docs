# VIDU Rest API v1

### Authentication

The Vidu API uses API Keys to authenticate requests.

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

`POST https://www.vidu.io/api/v1/jobs`

Enqueues a personalized [video](https://www.vidu.io/video) / [meme](https://www.vidu.io/memes) / [Peronsal GIF](https://www.vidu.io/personal-gifs) job.  

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

```
RESPONSE
{
	"id": 7654321,
	"status": "queued",
	"type": "job",
	"project": {
		"id": 26896,
		"name": "REST API Sample Video Recording",
		"type": "project",
		"project_type": "video"
	},
	"outputs": null,
	"completed_at": null,
	"inserted_at": "2023-09-21T12:44:00.765698Z",
	"view_key": "zeawsYJRbDlv",
	"inputs": {
		"website_1_url": "www.pusher.com",
		"website_2_url": "www.vidu.io"
	}
}
```

`GET https://www.vidu.io/api/v1/jobs/7654321`

...



