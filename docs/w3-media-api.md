# WBMA Media REST API

Based on ImageRekt api by: Juhani Lavonen, Matti Mäki-Kihniä & Mikael Gousetis

**NOTE**: API and the associated database is active for this course only. It's not a permanent storage for any files and will be cleaned/cleared on regular basis. 

### Base URLs

Api: http://util.mw.metropolia.fi/ImageRekt/api/v2/

Media folder: http://util.mw.metropolia.fi/uploads/


### Authentication 

There is **NO** real world authentication available. 

All passwords are sent in clear text. **Use dummy passwords only!**


## Usage

Documentation (and api itself) is still work on progress. Use Postman (http://www.getpostman.com/) to test features and report bugs to matti. 

All input values must be validated on client side.

### Users

#### Registration

POST `register`

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

#### Login

POST `login`

request content-type: application/x-www-form-urlencoded

Required form parameters:

- username
- password

**Response**: user id if login ok, example:

```js
{
  "user-id": 11,
  "status": "login ok"
}

```

#### List all users in service

GET `users`

**Response**: json array, example:

```js
[
  {
    "user": "Nnnnn Mmmmm",
    "email": "nn.mm@example.com",
    "uid": 20
  },
  {
    "user": "Another One",
    "email": "another.user@example.com",
    "uid": 21
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
  "user": "Another One",
  "email": "another.user@example.com",
  "uid": 21
}
```

#### Remove user

coming


### Files

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
{"file_id": "69"}
```

#### List all files in service

GET `files`

**Response**: json array, example:

```js
[
  {
    "path": "image.png",
    "title": "Name",
    "iid": 33,
    "type": "image"
  },
  {
    "path": "picture.jpg",
    "title": "Art",
    "iid": 32,
    "type": "image"
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
  "type": "image"
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
  "iid": 44
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
    "iid": 66,
    "type": "image"
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "iid": 65,
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
    "iid": 66,
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "iid": 65,
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
    "iid": 66,
    "type": "image"
  },
  {
    "path": "noidea.jpg",
    "title": "No idea",
    "iid": 65,
    "type": "image"
  }
]
``` 

### Comments

coming


