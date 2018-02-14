class: center, middle

# WBMA

## 5/2017

---

# Media Player

### Task: Create component for viewing single media files

1. Use the previous [exercise](w3-upload.md) as a starting point and develop it further
1. Create a new component/page for viewing single media files. Features:
    - get a single file from API
    - depending on file type use `<img>`, `<video>` or `<audio>` to show/play media file
        - <http://www.w3schools.com/tags/tag_video.asp>
        - <http://www.w3schools.com/tags/tag_audio.asp>  
    - show also other data related to the media file:
        - title
        - description
        - user (to get username you need to request [User endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-User-GetUser) using media file's `user_id`)
        - likes (request [Favourite endpoint](http://media.mw.metropolia.fi/wbma/docs/#api-Favourite) on the media api)
        - liked by user
1. Some help:
    - Add parameters to routerlink: `['/player', media.id]`
    - To use parameters:

_app.module.ts_

```
const routeConfig = [
...
    {
        path: 'player/:fileId',
        component: SomeComponent
    }
...
];
```

_some.component.ts_
```
    constructor(
    ...
    private route: ActivatedRoute,
    ...
    ) { }
```

```
    this.route.params.subscribe((params: any) => {
        console.log(params)
    });
```
