---
title: unstop
x-toc-enable: false
...

unstop
=========================================

I wrote a python script to perform neural style transfer.
The project was a good learning experience, I knew almost nothing about
python, neural networks or tensors. The code here is static and for
demonstration purposes only, up to date source code is available
[here](https://github.com/duncanldaho/unstop).[^1]


First the python modules need to be imported.
```
import os
import tensorflow as tf
import tensorflow_hub as hub
```


Then several functions are defined. This first function validates the user input
to make sure a real file is chosen. I'm not sure if it is "best practice" to
use an `elif` statement that loops back into the original function, but it
works.
```
def extension_check(user_input):
    if os.path.isfile(user_input):
        return user_input
    else:
        print("Invalid input.")
        user_input = extension_check(input("Image path: "))
        return user_input
```


A function to resize the style image is necessary since the model was trained on
an image that is 256x256.
```
def resize(image):
    image = tf.image.resize(
        image, (256, 256), preserve_aspect_ratio=True, antialias=True
    )
    return image
```

This next function decodes the JPEG data. A quick note on fixed and floating
point numbers. JPEGs use an 8 bit unsigned integer: 256 values can be
represented in base-2 with 8 bits, unsigned means those
values can only be positive, and integers are of course whole numbers.

**Fixed point** numbers are very *accurate*. They have a specific number of bits
reserved for the integer **and** a specific number of bits reserved for the
fraction. This comes at the cost of range, meaning you can represent fewer
values with the same given number of bits.

**Floating point** numbers are fundamentally different from fixed point,
in that the decimal point "floats". It can be placed anywhere relative to the
significant digits of the number. This means values are approximated, less
accurate but more precise. Floating point numbers are represented approximately,
and a larger range can be represented with the same given number of bits.


The JPEG `uint8` data is cast to `float32`. The RGB values can be [0,255],
so they are normalized by dividing by 255. Neurons can only process values
between [0,1].

These steps so far deliver a three dimensional array. An "empty" batch dimension
is added since the model expects this data shape.
```
def preprocess(image):
    image = tf.io.decode_jpeg(image, channels=3)
    image = tf.cast(image, tf.float32) / 255.0
    image = tf.expand_dims(image, axis=0)
    return image
```


The last function performs the opposite of the previous function. It removes the
batch dimension, coverts from [0,1] back to [0,255] RGB, casts the data from
`float32` to `uint8`, and then encodes the data back into a JPEG file.
```
def postprocess(image):
    """Remove batch dim., convert to RGB, cast to uint8, encode JPEG data."""
    image = tf.squeeze(image, axis=None) * 255.0
    image = tf.cast(image, tf.uint8)
    image = tf.io.encode_jpeg(image, quality=95)
    return image
```


Last of all is the actual code. It asks the user to specify the path to the
images, utilizing the first function to make sure a real file is chosen. It
loads the data, performs the functions in the appropriate order, and then
finally runs the two sets of data (each image) through the tensorflow model.
```
content_path = extension_check(input("Content image path: "))
style_path = extension_check(input("Style image path: "))
stylized_path = input("Write path: ")

content = tf.io.read_file(content_path)
style = tf.io.read_file(style_path)

hub_module = hub.load(
    "https://tfhub.dev/google/magenta/arbitrary-image-stylization-v1-256/2"
)

outputs = hub_module(preprocess(content), resize(preprocess(style)))
tf.io.write_file(stylized_path, postprocess(outputs))
```


The tensorflow model is a bit of a mystery to me. It passes the data through the
neural network and does some complicated maths to "extract" styles from one
image and add them to another.


A few things to look into:

 * Casting to different data type and/or encoding into different file types
 * Best practices in python, finding ways to improve performance, rearranging
the functions to be more intuitive
 * Setting the `preserve_aspect_ratio` and `antialias` options to true/false.
 * Replacing `tf.expand_dims` with `tf.reshape`

I would like to train my own models to gain a better understanding of neural
networks. I think it would be extremely worthwhile to make a network for audio
neural style transfer. All audio projects that I have come across use lossy
means of passing the audio data to the neural network. After I get around to
audio style transfer, A/V might be the next big project to work on.

[^1]: Source code is available under the [GPLv3 License](/licenses/license.html).
