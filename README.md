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

```
apt-get install ImageMagick
```

```
yum install ImageMagick
```

### MacOS

 ```
 brew install imagemagick
 ```

### Linux
 

#### Memory Constraints

https://github.com/google/sanitizers/wiki/AddressSanitizer

#### Capabilities

IM capabilities:

Animation,Color management,


### Info

* [`convert info`](http://www.imagemagick.org/script/index.php) shows convert info.


### Scripts


#### TIFF to PNG:

```
mogrify -background black -format png -depth 8  Data/Training/Images/cancer_subset00/*.tiff
```

####  SVG to PNG:

```
mogrify -background black -format png -depth 8 Data/Training/Labels/cancer_subset00/*.svg
```

####  JPG to jpg:

```
mogrify -format jpg *.JPG
```

####  webp to jpg:

```
convert input.webp output.jpg
```

```
mogrify -format JPG *.webp
```
#### Resize:

```
mogrify -resize 50% Data/Training/Images/cancer_subset00/*.png
```

``
mogrify -resize 100% --transparent -strip -quality 90  Data/Training/Images/cancer_subset00/*.png
``

#### jpeg reduce filesize

``
convert -resize 100%  -strip -quality 90  input.jpg out.jpg
``

#### png transpacent

 ``
convert -resize 100% -transparent  -strip -quality 90  input.png out.png
``

@see: http://www.imagemagick.org/script/command-line-options.php#quality

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

```
 mogrify -rotate 90 *.jpg
```

#### Rename with prefix

```
for filename in *.png; do mv "$filename" "prefix_$filename"; done;
```

#### split big image to small pieces

```
convert -crop 50%x100% input.png output.png
```

```
convert rose: -crop 23x15  +repage  +adjoin  rose_23x15_%02d.gif
```


#### Get image size, channel, alpha, depth, DPI

```
identify -format '%w X %h %[channels] %[bit-depth] %x x %y\n' input.jpeg
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

#### Background Transparent

```
convert input-with-solid-white-background-color.jpg -transparent white output-transparent.jpg
```

#### append photos horizontally

```
convert *.jpg -append full_horizontally.jpg
```
#### append photos vertically

```
convert *.jpg +append full_vertically.jpg
```

#### merge images


```

  montage balloon.gif medical.gif present.gif logo: \
          -geometry 48x48+2+2   montage_geom_size.jpg
```

#### colorspace

 sRGB to RGB
```
magick input.tif -colorspace RGB output.tif
```

### rename filenames

```
for f in *.jpg; do mv "$f" "$(echo "$f" | sed s/IMG/VACATION/)"; done
```

@more : https://legacy.imagemagick.org/Usage/montage/

## Contributing

Here's how to contribute to this cheat sheet.

### Open README.md

### Edit Page

### Make Changes and Commit

I will be greatly appreciated.

## References

http://www.imagemagick.org/script/index.php

http://www.fmwconcepts.com/imagemagick/fisheye2rect/index.php

http://www.fmwconcepts.com/imagemagick/rotate3D/index.php

speed up mogify: http://www.graphicsmagick.org/formats.html

https://legacy.imagemagick.org/discourse-server/viewtopic.php?t=21281

https://legacy.imagemagick.org/Usage/crop/#crop_tile
