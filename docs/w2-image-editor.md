class: center, middle

# Image Editor

## 2/2017

---
1. Clone this repo: https://github.com/ilkkamtk/ngImageEditor.git
2. Run `npm install` to load neccessary packages
3. Follow teachers instructions and comments in *.component.ts and *.service.ts files to load an image to canvas element and to change brightess and contrast of the image.
4. Use the BrightContrastComponent as an example to create a color filter and autocontrast. Use the formulas below.

## Extra 

Add grayscale conversion (checkbox). The human eye sees green a bit better than red and blue, so use luma coefficients to compensate that:
- R: 0.2126
- G: 0.7152
- B: 0.0722
___

### Formulas:
#### Brightness/contrast:

`Po = (P - 128) * C + 128 + B`

P = Pixel value

C = Contrast (range input 0-10, step 0.1)

B = brightness (range input -255 - 255, step 1)

#### Color filter: 

`Po = P + R / (101 - S)`

P = Pixel value

R = color value R/G/B (3 range inputs 0-255, step 1)

S = Strength (range input 0-100, step 1)



#### Autocontrast (checkbox):

`Po = (P - mi)/(ma - mi) * 255`

P = Pixel value

mi = minimum pixel value

ma = maximum pixel value

### Links:
- [Canvas](http://www.w3schools.com/html/html5_canvas.asp)
- [FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)
- [Image Editing Tutorial](https://www.html5rocks.com/en/tutorials/canvas/imagefilters/)
- [WebGL library for image editing](http://evanw.github.io/glfx.js/)
