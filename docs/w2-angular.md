# Angular image editor exercise

### Starting point

Clone repo from: https://github.com/ilkkamtk/imageEditor-start/

`npm install && bower install`


### Step 1 (Wednesday)

Example solution: https://github.com/ilkkamtk/imageEditor-start/tree/1st-step

It's a new branch in the same repo. You can fethch the new branch to your local branch using git:

```sh
# cd to project directory
# first save your own local changes
git add .
git commit -m "my changes"

# pull new stuff from server:
git pull
# activate the fetched branch
git checkout 1st-step 

```
 

### Step 2 (Thursday)

TODO:

- fix image ratio -> use image size as canvas size
- Add functionality to brightness & contrast sliders 
   - create a new function to scope
   - read the pixels of an image and change the values one by one
   - update canvas

tip: http://code.tutsplus.com/tutorials/canvas-from-scratch-pixel-manipulation--net-20573 