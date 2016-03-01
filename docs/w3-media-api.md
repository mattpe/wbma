# WBMA Media REST API

Based on ImageRekt api by: Juhani Lavonen, Matti Mäki-Kihniä & Mikael Gousetis

**NOTE**: API and the associated database is active for this course only. It's not a permanent storage for any files and will be cleaned/cleared on regular basis. 

## Changelog

#### 2016-02-11

- added _get latest files_ method

#### 2016-02-09

- added thumbnail images for files 
  - thumbnails are generated automatically when image file is uploaded
  - full size screen capture and thumbnails are generated automatically when video file is uploaded
- added _get all comments_ method
- added file search
- fixed bug: file upload doesn't accept empty parameter values any more 

#### 2016-02-02

- mime type property added to files. 
  - api solves mime type automatically after upload
- commenting of files added
- some minor fixes
  
#### 2016-01-28

- Property names in responses fixed to follow generic json naming conventions
  - `user` -> `username` or `userId`  depending on context
  - `iid` -> `fileId`
- Added `userId` to file requests 

## Base URLs

**REST API**: http://util.mw.metropolia.fi/ImageRekt/api/v2/

**Media folder**: http://util.mw.metropolia.fi/uploads/


## Authentication 

There is **NO** real world authentication available. 

All passwords are sent in clear text. **Use dummy passwords only!**


## Usage

Use [base url](http://util.mw.metropolia.fi/ImageRekt/api/v2/) + path

Example request: _GET_ http://util.mw.metropolia.fi/ImageRekt/api/v2/file/511

File paths are relative to [media folder](http://util.mw.metropolia.fi/uploads/): e.g: http://util.mw.metropolia.fi/uploads/zf8b1v-beach.jpg

Image/video thumbnails are placed in `thumbs/` sub folder and prefixed with `tn<size>_` where size options are 160, 320 and 640. Videos have also suffix `.png` and a full size screen capture image with prefix `sc_`. E.g. http://util.mw.metropolia.fi/uploads/thumbs/tn160_r1gpm6-dog.mp4.png

Documentation (and api itself) is still work in progress. Postman (http://www.getpostman.com/) can be used to test features easily. Report bugs to Matti. 

All user input values should always be validated on client side before making an http request to api.

### Users

#### Registration

**POST** `register` (combine with base url -> http://util.mw.metropolia.fi/ImageRekt/api/v2/register)

request content-type: application/x-www-form-urlencoded

Required form parameters:

- username
- password
- email

**Response**: status or error, examples:

```js
{
  "status": "ok",
  "message": "user nnnn added"
}
```
```js
{
  "error": "username already exists"
}

```

Check [tips](#post-data) section to see an example

#### Check if username already exists

**POST** `user/exists`

request content-type: application/x-www-form-urlencoded

Required form parameters:

- username

**Response**: json object, example:

```js
{
  "userFound": true
}

```

#### Login

**POST** `login`

request content-type: application/x-www-form-urlencoded

Required form parameters:

- username
- password

**Response**: user id if login ok, example:

```js
{
  "userId": 11,
  "status": "login ok"
}

```

#### List all users in service

**GET** `users`

**Response**: json array, example:

```js
[
  {
    "username": "Nnnnn Mmmmm",
    "email": "nn.mm@example.com",
    "userId": 20
  },
  {
    "username": "Another One",
    "email": "another.user@example.com",
    "userId": 21
  }
]
```

#### Get a user by id

**GET** `user/{id}`

Parameters: 
- id: user id

**Response**: json object, example:

```js
{
  "username": "Another One",
  "email": "another.user@example.com",
  "userId": 21
}
```

#### Remove user

coming


### Files

_path_ property in responses refers to _filename_ in media folder: `http://util.mw.metropolia.fi/uploads/<filename>`

#### Upload a file

**POST** `api/v2/upload`

request content-type: multipart/form-data

maximum file size: ~100 megabytes

Required parameters:

- file: the file itself
- user: user id
- title: file title text
- description: file description text
- type: file type text (image/video/audio)

**Response**: file id if success, example:

```js
{
  "fileId": "69"
}
```

#### List all files in the service

**GET** `files`

**Response**: json array, example:

```js
[
  {
    "path": "ox8hzrw14jay.jpg",
    "title": "Bear",
    "fileId": 729,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_ox8hzrw14jay.jpg",
      "medium": "thumbs/tn320_ox8hzrw14jay.jpg",
      "large": "thumbs/tn640_ox8hzrw14jay.jpg"
    },
    "userId": 12
  },
  {
    "path": "rpsvmnlg1kb3.png",
    "title": "Skeletor",
    "fileId": 728,
    "type": "image",
    "mimeType": "image/png",
    "thumbNails": {
      "small": "thumbs/tn160_rpsvmnlg1kb3.png",
      "medium": "thumbs/tn320_rpsvmnlg1kb3.png",
      "large": "thumbs/tn640_rpsvmnlg1kb3.png"
    },
    "userId": 20
  }
]
```

#### List latest files in the service

**GET** `files/latest/{number}`

Parameters: 
- number: number of files in response

**Response**: json array, example:

```js
[
  {
    "path": "ox8hzrw14jay.jpg",
    "title": "Bear",
    "fileId": 729,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_ox8hzrw14jay.jpg",
      "medium": "thumbs/tn320_ox8hzrw14jay.jpg",
      "large": "thumbs/tn640_ox8hzrw14jay.jpg"
    },
    "userId": 12
  },
  {
    "path": "rpsvmnlg1kb3.png",
    "title": "Skeletor",
    "fileId": 728,
    "type": "image",
    "mimeType": "image/png",
    "thumbNails": {
      "small": "thumbs/tn160_rpsvmnlg1kb3.png",
      "medium": "thumbs/tn320_rpsvmnlg1kb3.png",
      "large": "thumbs/tn640_rpsvmnlg1kb3.png"
    },
    "userId": 20
  }
]
```

#### Get a file by id

**GET** `file/{id}`

Parameters: 
- id: file id

**Response**: json object, example:

```js
{
  "path": "filename.jpg",
  "title": "Title of this image",
  "description": "This is the description of the image",
  "uploadTime": "Mon Feb 01 16:24:59 EET 2016",
  "type": "image",
  "mimeType": "image/jpeg",
  "thumbNails": {
    "small": "thumbs/tn160_filename.jpg",
    "medium": "thumbs/tn320_filename.jpg",
    "large": "thumbs/tn640_filename.jpg"
  },
  "userId": 12
}
```

#### Get a random file 

**GET** `file/random`

Parameters: 
- id: file id

**Response**: json object, example:

```js
{
  "path": "filename.jpg",
  "title": "Title of this image",
  "description": "This is the description of the image",
  "type": "image",
  "mimeType": "image/jpeg",
  "thumbNails": {
    "small": "thumbs/tn160_filename.jpg",
    "medium": "thumbs/tn320_filename.jpg",
    "large": "thumbs/tn640_filename.jpg"
  },
  "fileId": 44,
  "userId": 12
}
```

#### List all files by a user

**GET** `files/user/{user}`

Parameters: 
- user: user id

**Response**: json array, example:

```js
[
  {
    "path": "koala.jpg",
    "title": "koala",
    "fileId": 66,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_koala.jpg",
      "medium": "thumbs/tn320_koala.jpg",
      "large": "thumbs/tn640_koala.jpg"
    }
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "fileId": 65,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_noidea.jpg",
      "medium": "thumbs/tn320_noidea.jpg",
      "large": "thumbs/tn640_noidea.jpg"
    }
  }
]
```

#### List all files filtered by file type

**GET** `files/type/{type}`

Parameters: 
- type: file type (image/audio/video)

**Response**: json array, example:

```js
[
  {
    "path": "koala.jpg",
    "title": "koala",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_koala.jpg",
      "medium": "thumbs/tn320_koala.jpg",
      "large": "thumbs/tn640_koala.jpg"
    },
    "fileId": 66,
    "userId": 12
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_noidea.jpg",
      "medium": "thumbs/tn320_noidea.jpg",
      "large": "thumbs/tn640_noidea.jpg"
    },
    "fileId": 65,
    "userId": 12
  }
]
```

#### File title search 

**POST** `files/search/title`

request content-type: application/x-www-form-urlencoded

Required parameters: 
- title: search string

**Response**: json array, example:

```js
[
  {
    "path": "ytloe2-port-st-java.jpg",
    "title": "Coffee",
    "fileId": 71,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_ytloe2-port-st-java.jpg",
      "medium": "thumbs/tn320_ytloe2-port-st-java.jpg",
      "large": "thumbs/tn640_ytloe2-port-st-java.jpg"
    },
    "userId": 3
  },
  {
    "path": "ptl0dx-airtrick.jpg",
    "title": "coffee drinker",
    "fileId": 72,
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_ptl0dx-airtrick.jpg",
      "medium": "thumbs/tn320_ptl0dx-airtrick.jpg",
      "large": "thumbs/tn640_ptl0dx-airtrick.jpg"
    },
    "userId": 12
  }
]
```

#### File description search 

**POST** `files/search/desc`

request content-type: application/x-www-form-urlencoded

Required parameters: 
- desc: search string

**Response**: json array, example:

```js
[
  {
    "path": "ptl0dx-airtrick.jpg",
    "title": "snowboarder",
    "description": "jump",
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_ptl0dx-airtrick.jpg",
      "medium": "thumbs/tn320_ptl0dx-airtrick.jpg",
      "large": "thumbs/tn640_ptl0dx-airtrick.jpg"
    },
    "fileId": 72,
    "userId": 1
  },
  {
    "path": "aom5mo-air1.jpg",
    "title": "trick",
    "description": "jumping higher",
    "type": "image",
    "mimeType": "image/jpeg",
    "thumbNails": {
      "small": "thumbs/tn160_aom5mo-air1.jpg",
      "medium": "thumbs/tn320_aom5mo-air1.jpg",
      "large": "thumbs/tn640_aom5mo-air1.jpg"
    },
    "fileId": 73,
    "userId": 1
  }
]
```



#### Remove a file

coming

### Likes

#### Like a file

**GET** `like/{file}/{user}`

Parameters: 

- file: file id
- user: user id

**Response**: json object, example:

```js
{
  "status": "liked already"
}
```

#### Unlike a file

**GET** `unlike/{file}/{user}`

Parameters: 

- file: file id
- user: user id

**Response**: json object, example:

```js
{
  "status": "unliked"
}
```

#### List files liked by a user

**GET** `likes/user/{id}`

Parameters: 
- id: user id

**Response**: json array, example:

```js
[
  {
    "path": "Koala.jpg",
    "title": "koala",
    "fileId": 66,
    "type": "image"
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "fileId": 65,
    "type": "image"
  }
]
``` 

### Comments

#### Add a comment to a file 

**POST** `comment/file/{id}`

request content-type: application/x-www-form-urlencoded

Parameters: 
- id: file id

Required post parameters:
- user: user id
- comment: comment content 

**Response**: json object, example:

```js
{
  "status": "comment added"
}
```

#### Get all comments

**GET** `comments`

**Response**: json array, example:

```js
[
  {
    "comment": "nice file",
    "username": "SomeUser",
    "userId": 13,
    "fileId": 213,
    "time": "Tue Feb 02 15:56:16 EET 2016"
  },
  {
    "comment": "funny cats",
    "username": "CatLover99",
    "fileId": 3,
    "userId": 23,
    "time": "Tue Feb 02 15:56:34 EET 2016"
  }
]
```

#### Get all comments of a file 

**GET** `comments/file/{id}`

Parameters: 
- id: file id

**Response**: json array, example:

```js
[
  {
    "comment": "nice file",
    "username": "SomeUser",
    "userId": 13,
    "time": "Tue Feb 02 15:56:16 EET 2016"
  },
  {
    "comment": "funny cats",
    "username": "CatLover99",
    "userId": 23,
    "time": "Tue Feb 02 15:56:34 EET 2016"
  }
]
```


## Tips

#### Post data 

Simplified angular example of sending  data in _application/x-www-form-urlencoded_ format.

[$httpParamSerializer](https://docs.angularjs.org/api/ng/service/$httpParamSerializer) converts data from json object to form data fields. 

Register a new user:

```js
$http({
  method: 'POST',
  url: restApiBaseUrl + 'register',
  headers: {'Content-Type' : 'application/x-www-form-urlencoded'},
  data: $httpParamSerializer({
          username: "batman",
          email: "batman@example.com",
          password: "stupidpassword"
        })
}).then(function (response) {
  console.log(response.data);

}, function (error) {
  console.log(error);
});
```

#### Dates & times

Time properties in json responses are created by Java's `Date.toString()` and the format is not the easiest one to utilise. One option to parse and format times is to use [moment.js](http://momentjs.com/) library.

e.g. Angular custom filter with moment.js:

```js
angular.module('app')
  .filter('javaDate', function () {
    return function (javaDateString) {
      return moment(javaDateString, "ddd MMM DD HH:mm:ss zzz gggg")
        .format("ddd D.M.YYYY - HH:mm");
    };
  });
```

#### Formdata and image from canvas

http://stackoverflow.com/questions/4998908/convert-data-uri-to-file-then-append-to-formdata
