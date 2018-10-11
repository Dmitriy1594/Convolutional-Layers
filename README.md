# NeiroGraph
## Course project

## Image convolution
The convolution is identical to the operation of the clipping but the core is mirrored during convolution

### Fighting the lack of pixels
* Filling with a constant
* Taking the nearest value
* Boundary mirroring

### Kernel
- [Different_kernels](https://en.wikipedia.org/wiki/Kernel_(image_processing))

#### How it works?
<img src='theory/stride1.gif'>

<img src='theory/stride2.gif'>

#### RGB and Kernel
<img src='theory/rgb.gif'>

## kernels
In this directory you can find different kernels to your images.

## pictures
In this directory you can find images for your tests.

## src
In directory you should have 2 fies:
- [x] convolve3.py
- [x] convolve2.py
- [x] convolve.py

## convolve3.py
### RGB convolution layers for all channels! 
Also you can read your picture in one channel!

### kernel.kern3
You can write in file 3 kernels for all channels! First kernel (red), midlle (green), last (blue)
```
0 0 0
0 1 0
0 0 0

0 0 0 0 0
0 0 0 0 0
0 0 1 0 0
0 0 0 0 0
0 0 0 0 0

0 0 0
0 1 0
0 0 0
```
### kernel.kern
It's similarly as in convolve2.py and convolve.py

### Create folder with all result files
The last argument in the command line is a name of your folder.
#### If you write kernel.kern:
In your folder you should have 2 fies:
- [x] grayorig.txt
- [x] grayorig.png
- [x] result.txt
- [x] result.png
#### If you write kernel.kern3:
In your folder you should have 10 fies:
- [x] r.txt                 // red channel: original matrix
- [x] result_r.txt          // red channel: result matrix
- [x] result_r.png          // red channel: plot result
- [x] g.txt                 // green channel: original matrix
- [x] result_g.txt          // green channel: result matrix
- [x] result_g.png          // green channel: plot result
- [x] b.txt                 // blue channel: original matrix
- [x] result_b.txt          // blue channel: result matrix
- [x] result_b.png          // blue channel: plot result
- [x] result.png            // result convolutional layers

### Run the script from terminal or command line
Run multichannel:
```
python conv.py 1.jpg kernel.kern3 super
```
Run one channel:
```
python conv.py 1.jpg kernel.kern super
```

## convolve2.py
### New feature!
You can write in kernel file fractional numbers!
```
-1 -1 -1
-1 8/9 -1
-1 -1 -1
```
### Run the script from terminal or command line
```
python convolve.py 12.png kernel.kern
```
### convolution2d
It's similarly as in convolve.py

## convolve.py
### Attention!
### Write your kernel correctly:
Only integer numbers
```
-1 -1 -1
-1 8 -1
-1 -1 -1
```
### Run the script from terminal or command line
```
python convolve.py -i 12.png -f kernel.kern
```
#### OR
```
python convolve.py --image 12.png --file kernel.kern
```

### convolution2d in convolve.py and convolve2.py
```python
def convolve2d(image, kernel):
    # Flip the kernel
    kernel = np.flipud(np.fliplr(kernel))
    # convolution output
    output = np.zeros_like(image)
    # Add zero padding to the input image
    image_pad = np.zeros((image.shape[0] + 2, image.shape[1] + 2))
    image_pad[1:-1, 1:-1] = image

    # Loop over every pixel of the image
    for x in range(image.shape[1]):
        for y in range(image.shape[0]):
            # element-wise multiplication of the kernel and the image
            output[y, x] = (kernel * image_pad[y:y + 3, x:x + 3]).sum()
    return output

# Get a numpy array of size [image_height, image_width]
image_sharpen = convolve2d(img, kernel)
```
