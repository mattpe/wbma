# WBMA Media REST API

Based on ImageRekt api by: Juhani Lavonen, Matti Mäki-Kihniä & Mikael Gousetis

**NOTE**: API and the associated database is active for this course only. It's not a permanent storage for any files and will be cleaned/cleared on regular basis. 

## Changelog

#### 28.1.2016

- Property names in responses fixed to follow generic json naming conventions
  - `user` -> `username` or `userId`  depending on context
  - `iid` -> `fileId`
- Added `userId` to file requests 

## Base URLs

Api: http://util.mw.metropolia.fi/ImageRekt/api/v2/

Media folder: http://util.mw.metropolia.fi/uploads/


## Authentication 

There is **NO** real world authentication available. 

All passwords are sent in clear text. **Use dummy passwords only!**


## Usage

Use base url + path

Example request: GET http://util.mw.metropolia.fi/ImageRekt/api/v2/file/3

File paths are relative to media folder: e.g: http://util.mw.metropolia.fi/uploads/ring5.jpg

Documentation (and api itself) is still work on progress. Use Postman (http://www.getpostman.com/) to test features and report bugs to matti. 

All input values must be validated on client side.

### Users

#### Registration


POST `register` (combine with base url -> http://util.mw.metropolia.fi/ImageRekt/api/v2/register)

request content-type: application/x-www-form-urlencoded

Required form parameters:

- username
- password

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

POST `user/exists`

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

POST `login`

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

GET `users`

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

GET `user/{id}`

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

POST `api/v2/upload`

request content-type: multipart/form-data

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

#### List all files in service

GET `files`

**Response**: json array, example:

```js
[
  {
    "path": "image.png",
    "title": "Name",
    "fileId": 33,
    "type": "image",
    "userId": 12
  },
  {
    "path": "picture.jpg",
    "title": "Art",
    "fileId": 32,
    "type": "image",
    "userId": 12
  }
]
```

#### Get a file by id

GET `file/{id}`

Parameters: 
- id: file id

**Response**: json object, example:

```js
{
  "path": "filename.jpg",
  "title": "Title of this image",
  "description": "This is the description of the image",
  "type": "image",
  "userId": 12
}
```

#### Get a random file 

GET `file/random`

Parameters: 
- id: file id

**Response**: json object, example:

```js
{
  "path": "filename.jpg",
  "title": "Title of this image",
  "description": "This is the description of the image",
  "type": "image",
  "fileId": 44,
  "userId": 12
}
```

#### List all files by a user

GET `files/{user}`

Parameters: 
- user: user id

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

#### List all files filtered by file type

GET `files/type/{type}`

Parameters: 
- type: file type (image/audio/video)

**Response**: json array, example:

```js
[
  {
    "path": "Koala.jpg",
    "title": "koala",
    "fileId": 66,
    "userId": 12
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "fileId": 65,
    "userId": 12
  }
]
```

#### Remove a file

coming

### Likes

#### Like a file

GET `like/{file}/{user}`

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

GET `unlike/{file}/{user}`

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

GET `likes/user/{id}`

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

coming


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
