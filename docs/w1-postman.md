class: center, middle

# Using Postman to explore APIs

## 1/2019

---

# Task 1: Play with the Postman

1. [Get Postman](https://www.getpostman.com/) and take a look at [docs & tutorials](https://www.getpostman.com/docs/).
2. Check [Media API docs](http://media.mw.metropolia.fi/wbma/docs/) Base URL for the api endpoints is <http://media.mw.metropolia.fi/wbma> 

Use Postman to:

3. `GET` a list of files 
4. Create an user account (`POST users/`) using your metropolia.fi email (insert data in request body and use content-type: _x-www-form-urlencoded_)
5. `POST login/` using your account and save the token string from the response
6. Add the token to your following request headers (key name: _x-access-token_)
7. Try `PUT users/` to change your password and log in again to get a new token
8. `POST media/` to upload a media file (use body content-type: _form-data_)
9. `POST comment/` to some other user's file
10. `PUT media` to change description of your file
11. `POST favourite` to like some file

**Submit your user_id AND username you made in bullet 4. to Oma assignment.**
