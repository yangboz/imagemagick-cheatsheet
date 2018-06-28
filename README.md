# ImageMagick Cheat Sheet

**Want to improve this cheat sheet?  See the [Contributing](#contributing) section!**

## Table of Contents

* [Why ImageMagick](#why-ImageMagick)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Best Practices](#best-practices)
* [Tips](#tips)
* [Contributing](#contributing)

## Why ImageMagick

Use ImageMagick® to create, edit, compose, or convert bitmap images. It can read and write images in a variety of formats (over 200) including PNG, JPEG, GIF, HEIC, TIFF, DPX, EXR, WebP, Postscript, PDF, and SVG. Use ImageMagick to resize, flip, mirror, rotate, distort, shear and transform images, adjust image colors, apply various special effects, or draw text, lines, polygons, ellipses and Bézier curves.

The functionality of ImageMagick is typically utilized from the command-line or you can use the features from programs written in your favorite language. Choose from these interfaces: G2F (Ada), MagickCore (C), MagickWand (C), ChMagick (Ch), ImageMagickObject (COM+), Magick++ (C++), JMagick (Java), JuliaIO (Julia), L-Magick (Lisp), Lua (LuaJIT), NMagick (Neko/haXe), Magick.NET (.NET), PascalMagick (Pascal), PerlMagick (Perl), MagickWand for PHP (PHP), IMagick (PHP), PythonMagick (Python), magick (R), RMagick (Ruby), or TclMagick (Tcl/TK). With a language interface, use ImageMagick to modify or create images dynamically and automagically.

TL;NR

## Prerequisites

### ColorSpace

### Image Processing

### Image format

TL;NR

## Installation

### Linux

???

### MacOS

 ```
 brew install imagemagick
 ```



### Linux



#### CPU Constraints

You can limit CPU, either using a percentage of all CPUs, or by using specific cores.  

#### Memory Constraints

You can also set [memory constraints]


#### Capabilities

IM capabilities:

Animation,Color management


### Info

* [`convert info`](https://docs.docker.com/engine/reference/commandline/ps) shows running containers.



### Scripts


#### TIFF to PNG:

```
mogrify -background black -format png -depth 8  Data/Training/Images/cancer_subset00/*.tiff
```

####  SVG to PNG:

```
mogrify -background black -format png -depth 8 Data/Training/Labels/cancer_subset00/*.svg
```

#### Resize:

```
mogrify -resize 50% Data/Training/Images/cancer_subset00/*.png
```

#### GrayScale

```
for file in Data/Training/Images/cancer_subset00/*.png; do convert $file  -colorspace Gray $file;done
```

#### SVG fill replace:

```
find ./ -type f -name '*.svg' | xargs -I{} sed -i_old -n -e 's/polygon fill="none"/polygon fill="white"/g;p;' {}
```

#### Gray to RGB

```
mogrify -type TrueColorMatte -define png:color-type=6  /Volumes/UUI/labels/normal/*.png

```
#### Rotate 90

```
mogrify -rotate 90 /Volumes/UUI/images/rotate90/*.png
```
#### Rename with prefix

```
for filename in *.png; do mv "$filename" "prefix_$filename"; done;
```
#### Flip

#### Flop

#### Resize

batch:

```
mogrify -resize 750x750\! *.jpg 
```
#### File Resize

```
mogrify -define jpeg:extent=5100kb *.png
```


## Contributing

Here's how to contribute to this cheat sheet.

### Open README.md

Click [README.md](https://github.com/wsargent/docker-cheat-sheet/blob/master/README.md) <-- this link

![Click This](images/click.png)

### Edit Page

![Edit This](images/edit.png)

### Make Changes and Commit

![Change This](images/change.png)

![Commit](images/commit.png)


## References

http://www.imagemagick.org/script/index.php

http://www.fmwconcepts.com/imagemagick/fisheye2rect/index.php

