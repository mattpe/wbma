# Angular image editor exercise

![Image editor screenshot](../images/image-editor-screenshot.png)

### Starting point

Clone repo from: https://github.com/ilkkamtk/imageEditor-start/

Install dependicies list in _package.json & bower.json_: `npm install && bower install`

[Ruby](https://www.ruby-lang.org/en/) is needed to install compass: `[sudo] gem install compass`

### Step 1 (Wednesday)

**TODO:** 

- Open an image file on editor and draw it on canvas
- Bind input values to controller's scope 

Example solution: https://github.com/ilkkamtk/imageEditor-start/tree/1st-step

It's a new branch in the same repo. You can fethch the new branch to your local (already cloned) repository using git:

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

**TODO**:

- fix image ratio -> use image size as canvas size
- Add functionality to brightness & contrast sliders 
   - create a new function to scope
   - read the pixels of an image and change the values one by one
   - update canvas

**tip**: http://code.tutsplus.com/tutorials/canvas-from-scratch-pixel-manipulation--net-20573 

### Step 3 (Friday)

**TODO**: Finalize it! 

