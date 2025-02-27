# ImageMagick Cheat Sheet

**Want to improve this cheat sheet? See the [Contributing](#contributing) section!**

## Table of Contents

* [Why ImageMagick](#why-imagemagick)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Basic Commands](#basic-commands)
* [Format Conversion](#format-conversion)
* [Resizing and Transformations](#resizing-and-transformations)
* [Color Adjustments](#color-adjustments)
* [Image Composition](#image-composition)
* [Text and Annotations](#text-and-annotations)
* [Special Effects](#special-effects)
* [Batch Processing](#batch-processing)
* [Animation and GIFs](#animation-and-gifs)
* [Image Analysis](#image-analysis)
* [Advanced Operations](#advanced-operations)
* [Best Practices](#best-practices)
* [Tips](#tips)
* [Troubleshooting](#troubleshooting)
* [Contributing](#contributing)
* [References](#references)

## Why ImageMagick

Use ImageMagick® to create, edit, compose, or convert bitmap images. It can read and write images in a variety of formats (over 200) including PNG, JPEG, GIF, HEIC, TIFF, DPX, EXR, WebP, Postscript, PDF, and SVG. Use ImageMagick to resize, flip, mirror, rotate, distort, shear and transform images, adjust image colors, apply various special effects, or draw text, lines, polygons, ellipses and Bézier curves.

The functionality of ImageMagick is typically utilized from the command-line or you can use the features from programs written in your favorite language. Choose from these interfaces: G2F (Ada), MagickCore (C), MagickWand (C), ChMagick (Ch), ImageMagickObject (COM+), Magick++ (C++), JMagick (Java), JuliaIO (Julia), L-Magick (Lisp), Lua (LuaJIT), NMagick (Neko/haXe), Magick.NET (.NET), PascalMagick (Pascal), PerlMagick (Perl), MagickWand for PHP (PHP), IMagick (PHP), PythonMagick (Python), magick (R), RMagick (Ruby), or TclMagick (Tcl/TK). With a language interface, use ImageMagick to modify or create images dynamically and automagically.

## Prerequisites

### ColorSpace

Understanding color spaces like RGB, CMYK, sRGB is helpful when working with ImageMagick.

### Image Processing

Basic knowledge of image processing concepts helps when using the more advanced features.

### Image Format

Familiarity with different image formats and their properties.

## Installation

### Linux (Debian/Ubuntu)

```bash
apt-get install imagemagick
```

### Linux (RHEL/CentOS)

```bash
yum install imagemagick
```

### MacOS

```bash
brew install imagemagick
```

### Memory Constraints

For memory-related issues: https://github.com/google/sanitizers/wiki/AddressSanitizer

## Basic Commands

### Show ImageMagick Info

```bash
convert -version
```

```bash
identify -list all
```

### Verify Installation

```bash
convert logo: logo.png
```

## Format Conversion

### TIFF to PNG

```bash
mogrify -background black -format png -depth 8 *.tiff
```

### SVG to PNG

```bash
mogrify -background black -format png -depth 8 *.svg
```

### JPG to jpg (Normalize Extension)

```bash
mogrify -format jpg *.JPG
```

### WebP to JPG

```bash
convert input.webp output.jpg
```

```bash
mogrify -format jpg *.webp
```

### DICOM to JPG

```bash
convert *.DCM output.jpg
```

### Multiple Images to PDF

```bash
convert *.jpg document.pdf
```

### PDF to Images (One Per Page)

```bash
convert -density 300 document.pdf page%03d.jpg
```

### High-Quality JPEG Conversion

```bash
convert input.png -quality 92 -sampling-factor 4:2:0 output.jpg
```

## Resizing and Transformations

### Resize by Percentage

```bash
mogrify -resize 50% *.png
```

### Resize to Exact Dimensions (Ignoring Aspect Ratio)

```bash
mogrify -resize 750x750\! *.jpg
```

### Create a Thumbnail (Preserving Aspect Ratio)

```bash
convert input.jpg -thumbnail 150x150 thumbnail.jpg
```

### Rotate Image

```bash
mogrify -rotate 90 *.jpg
```

### Flip (Vertical Mirror)

```bash
convert input.jpg -flip output.jpg
```

### Flop (Horizontal Mirror)

```bash
convert input.jpg -flop output.jpg
```

### Add Border

```bash
convert input.jpg -border 10 -bordercolor black output.jpg
```

### Crop Image

```bash
convert input.jpg -crop 300x200+50+50 output.jpg
```

### Split Large Image into Tiles

```bash
convert -crop 512x512 +repage large.tif tiles/image_%d.tif
```

### Create a 3D Rotation Effect

```bash
# Requires additional scripts
# See: http://www.fmwconcepts.com/imagemagick/rotate3D/index.php
```

## Color Adjustments

### Convert to Grayscale

```bash
convert input.jpg -colorspace Gray output.jpg
```

```bash
for file in *.png; do convert $file -colorspace Gray $file; done
```

### Convert from Grayscale to RGB

```bash
mogrify -type TrueColorMatte -define png:color-type=6 *.png
```

### Colorspace Conversion

```bash
convert input.tif -colorspace RGB output.tif
```

### Apply Color Profile Conversion

```bash
convert input.jpg -profile sRGB.icc -profile AdobeRGB.icc output.jpg
```

### Adjust Brightness and Contrast

```bash
convert input.jpg -brightness-contrast 10x15 output.jpg
```

### Invert Colors (Create Negative)

```bash
convert input.jpg -negate negative.jpg
```

### Make Background Transparent

```bash
convert input.jpg -transparent white output.png
```

### Apply Sepia Tone Effect

```bash
convert input.jpg -sepia-tone 80% sepia-output.jpg
```

## Image Composition

### Append Images Horizontally

```bash
convert *.jpg +append horizontally_appended.jpg
```

### Append Images Vertically

```bash
convert *.jpg -append vertically_appended.jpg
```

### Create a Montage

```bash
montage *.jpg -geometry 200x200+5+5 -background lightblue montage.jpg
```

### Create Composite with Overlay

```bash
composite -gravity center overlay.png base.jpg output.jpg
```

### Create Before/After Comparison

```bash
convert before.jpg after.jpg +append comparison.jpg
```

## Text and Annotations

### Add Text to Image

```bash
convert input.jpg -fill white -pointsize 24 -gravity southeast -annotate +10+10 'Copyright 2025' output.jpg
```

### Add Watermark

```bash
convert input.jpg -gravity southeast -stroke '#FFFFFF' -strokewidth 2 -annotate +5+5 'Watermark' -stroke none -fill '#FFFFFF88' -annotate +5+5 'Watermark' output.jpg
```

## Special Effects

### Apply Blur Effect

```bash
convert input.jpg -blur 0x8 blurred-output.jpg
```

### Create a Vignette Effect

```bash
convert input.jpg -vignette 0x20 vignette.jpg
```

### Apply Charcoal Sketch Effect

```bash
convert input.jpg -charcoal 2 sketch.jpg
```

### Create Polaroid-Style Image

```bash
convert input.jpg -bordercolor white -border 10 -background black -rotate 6 -background white -polaroid 10 polaroid.jpg
```

### Apply Fisheye Effect

```bash
# Requires additional scripts
# See: http://www.fmwconcepts.com/imagemagick/fisheye2rect/index.php
```

## Batch Processing

### Convert All Images in a Folder

```bash
mogrify -format jpg *.png
```

### Apply Same Edit to Multiple Images

```bash
mogrify -resize 800x600 -quality 85 *.jpg
```

### Batch Resize and Add Watermark

```bash
for file in *.jpg; do
  convert "$file" -resize 1024x768 -fill white -pointsize 20 -gravity southeast \
  -annotate +10+10 'Copyright 2025' "watermarked_$file"
done
```

### Rename Files with Prefix

```bash
for filename in *.png; do mv "$filename" "prefix_$filename"; done
```

### Rename Files by Pattern

```bash
for f in *.jpg; do mv "$f" "$(echo "$f" | sed s/IMG/VACATION/)"; done
```

### Reduce JPEG Filesize

```bash
convert -resize 100% -strip -quality 90 input.jpg output.jpg
```

### Create PNG with Transparency

```bash
convert -resize 100% -transparent -strip -quality 90 input.png output.png
```

## Animation and GIFs

### Create GIF from Sequence of Images

```bash
convert -delay 20 -loop 0 frame*.jpg animated.gif
```

### Extract Frames from Animated GIF

```bash
convert animated.gif -coalesce frame%03d.png
```

### Optimize GIF Filesize

```bash
convert input.gif -layers optimize optimized.gif
```

### Resize Animated GIF

```bash
convert input.gif -coalesce -resize 50% -layers optimize output.gif
```

## Image Analysis

### Get Basic Image Information

```bash
identify image.jpg
```

### Get Detailed Image Properties

```bash
identify -format '%w X %h %[channels] %[bit-depth] %x x %y\n' input.jpeg
```

### Show Verbose Image Information

```bash
identify -verbose image.jpg
```

### Calculate Image Statistics

```bash
convert image.jpg -format "%[mean] %[standard-deviation]" info:
```

### Check Image Histogram

```bash
convert image.jpg -define histogram:unique-colors=true histogram:info:
```

## Advanced Operations

### SVG Fill Replacement

```bash
find ./ -type f -name '*.svg' | xargs -I{} sed -i_old -n -e 's/polygon fill="none"/polygon fill="white"/g;p;' {}
```

### Limit Output Filesize

```bash
mogrify -define jpeg:extent=5100kb *.png
```

### Create Mosaic of Images

```bash
montage -geometry 200x200+5+5 -background lightblue *.jpg mosaic.jpg
```

## Best Practices

* Use GraphicsMagick for faster processing when applicable
* Use appropriate colorspace for your target medium
* Be mindful of memory usage for large images
* Set appropriate quality when saving to lossy formats

## Tips

* Use `-strip` to remove metadata and reduce file size
* When working with transparency, use PNG rather than JPG
* For complex scripts, consider using ImageMagick with shell scripting
* Use `mogrify` for in-place edits and `convert` for creating new files

## Troubleshooting

* For font configuration warnings: https://stackoverflow.com/questions/24712158/how-to-solve-imagemagicks-fontconfig-warning-ignoring-utf-8-not-a-valid-regi
* Check permissions for output directories
* Verify that your ImageMagick installation has the required delegates for specific formats
* If processing fails, try increasing memory limits in policy.xml

## Contributing

Here's how to contribute to this cheat sheet:

1. Fork the repository
2. Open README.md
3. Make your changes
4. Submit a pull request

Your contributions will be greatly appreciated!

## References

* Official Website: http://www.imagemagick.org/script/index.php
* Command-Line Options: http://www.imagemagick.org/script/command-line-options.php
* Fred's ImageMagick Scripts: http://www.fmwconcepts.com/imagemagick/
* GraphicsMagick: http://www.graphicsmagick.org/formats.html
* Legacy Forum: https://legacy.imagemagick.org/discourse-server/
* Crop & Tile Examples: https://legacy.imagemagick.org/Usage/crop/#crop_tile
* Montage Usage: https://legacy.imagemagick.org/Usage/montage/
