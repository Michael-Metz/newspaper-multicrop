# Table of Contents
1. [Introduction](#introduction)
2. [License](#license)
3. [Set Up & Installation](#setup-and-installation)
4. [Usage](#usage)
5. [Differences](#differences)
6. [My Workflow](#myworkflow)
7. [Disk Considerations](#disk-considerations)
8. [What Exactly The Script Does](#what-exactly-the-script-does)

<a name="introduction"></a>
# Introduction
newspaper-multicrop and newspaper-multicrop2 are bash shell scripts that create transparent crops, from a scanned image, that contain multiple newspaper clippings.

The scripts are built on top of *[imagemagick](https://www.imagemagick.org/script/index.php)* along with [freds weihaus's](http://www.fmwconcepts.com/imagemagick/),  *[multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php)* and *[multicrop2](http://www.fmwconcepts.com/imagemagick/multicrop2/index.php)* scripts
![Imgur](https://i.imgur.com/zsHbr5E.gif)

newspaper-multicrop and newspaper-multicrop2 differ from multicrop and multicrop2 in the following ways

1. You can use a custom mask, instead of having multicrop generate a mask
2. Borders are left transparent instead of white

<a name="license"></a>
# License
Use of newspaper-multicrop and newspaper-multicrop2 are subject, in a subordinate manner, to Fred Weinhaus's license which can be found at [http://www.fmwconcepts.com/imagemagick/](http://www.fmwconcepts.com/imagemagick/) and to the ImageMagick's license, which can be found at: [http://www.imagemagick.org/script/license.php](http://www.imagemagick.org/script/license.php)

**Freds scripts require licensing for commercial use. Therefore if you plan on using newspaper-multicrop, newspaper-multicrop2, multicrop, or mulitcrop2, commercially then you MUST contact [Fred](http://www.fmwconcepts.com/imagemagick/)**
<a name="setup-and-installation"></a>
# Set Up & Installation
> The following installation instructions are done under the ubunutu 16.04 operating system

## 1. Install ImageMagick
Look on [imagemagicks website](https://www.imagemagick.org/script/index.php) for installation instructions or if you use ubuntu, look below
#### Install with ubuntu's terminal
```sh
$ sudo apt-get update
$ sudo apt install imagemagick
```
## 2. Install Fred Weinhaus's multicrop & multicrop2 Scripts
##### Make a folder to store freds scripts
```sh
$ mkdir -p $HOME/bin/fredscripts
```
##### Download the scripts from [freds website](http://www.fmwconcepts.com/imagemagick) ([mulitcrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php), [multicrop2](http://www.fmwconcepts.com/imagemagick/multicrop2/index.php)) and move them to `$HOME/bin/fredscripts`
```sh
$ # Download the scripts
$ wget http://www.fmwconcepts.com/imagemagick/multicrop/multicrop
$ wget http://www.fmwconcepts.com/imagemagick/multicrop2/multicrop2

$ # Move them into folder
$ mv multicrop $HOME/bin/fredscripts/
$ mv multicrop2 $HOME/bin/fredscripts/
```
##### Make the scripts executable
```sh
$ sudo chmod -R +x $HOME/bin/fredscripts/
```
##### Add fredscripts to your path in `.profile`
```sh
$ cd $HOME
$ sudo nano .profile
```
`nano` opens a text editor

##### Add to your `.profile` as seen below

```
# add to PATH so it includes user's private bin directories
PATH="$HOME/bin:$HOME/.local/bin:$PATH"

#freds imagemagick scripts
export PATH="$HOME/bin/fredscripts:$PATH"
```
To save and exit the text editor, type `ctrl + x` followed by `y` then hit return

## 3. Install newspaper-multicrop & newspaper-multicrop2

##### Make a folder to store the scripts
```sh
$ mkdir -p $HOME/bin/michael-metz
```
##### Download the scripts and move them to `$HOME/bin/michael-metz`
```sh
$ # Clone the repo with git or download the scripts manually
$ git clone https://github.com/Michael-Metz/newspaper-multicrop.git
$
$ # Move them into folder
$ mv newspaper-multicrop/* $HOME/bin/michael-metz/
$ rm -rf newspaper-multicrop
```
##### Make the scripts executable
```sh
$ sudo chmod -R +x $HOME/bin/michael-metz/
```
##### Add my scripts to your path in `.profile`
```sh
$ cd $HOME
$ sudo nano .profile
```
`nano` opens a text editor

##### Add to your `.profile`

```
#michael-metz scripts
export PATH="$HOME/bin/michael-metz:$PATH"
```
To save and exit the text editor, type `ctrl + x` followed by `y` then hit return

<a name="usage"></a>

## 4. (optional) Install Fred Weinhaus's textdeskew script

since we already made the folder `fredscripts` and added it to our path, we just
 have to download the script to `fredscripts`.

##### Download the script from [freds website](http://www.fmwconcepts.com/imagemagick) ([textdeskew](http://www.fmwconcepts.com/imagemagick/textdeskew/index.php)), and move them to `$HOME/bin/fredscripts`
```sh
$ # Download the scripts
$ wget http://www.fmwconcepts.com/imagemagick/textdeskew/textdeskew
$
$ # Move them into folder
$ mv textdeskew $HOME/bin/fredscripts/
```
##### Make the script executable
```sh
$ sudo chmod -R +x $HOME/bin/fredscripts/
```

# Usage
### newspaper-multicrop
newspaper-multicrop separates images using multicrop requires 4 parameters

1. image
2. image mask (See *[Creating a Mask](#create-a-mask)* )
3. grid value(*Integer value 0 < gv < 100 passed to multicrop*)
4. deskew method (*Integer value either 0 or 1*)
    * 0: deskew; imagemagicks built in deskew; *faster*"
    * 1: textdeskew; Fred Weinhaus script must be installed; *slower but better*"

```sh
$ #newspaper-multicrop [image] [image mask] [grid value] [deskew-method]
$ newspaper-multicrop clippings.tif clippings_mask.png 10 0
```


### newspaper-multicrop2
newspaper-multicrop2 separates images using multicrop2 and requires requires 4 parameters

1. image
2. image mask (See *[Creating a Mask](#create-a-mask)* )
3. discard value(*Integer value 0 < dv passed to multicrop2*)
4. deskew method (*Integer value either 0 or 1*)
    * 0: deskew; imagemagicks built in deskew; *faster*"
    * 1: textdeskew; Fred Weinhaus script must be installed; *slower but better*"

```sh
$ #newspaper-multicrop2 [image] [image mask] [discard value] [deskew-method]
$ newspaper-multicrop2 clippings.tif clippings_mask.png 800 0
```

<a name="differences"></a>
# Differences
**newspaper-multicrop** splits images using **multicrop**

**newspaper-multicrop2** splits images using **multicrop2**

### multicrop vs multicrop2



**[multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php)** works by thresholding the image(making it black and white) then searches the image for white pixels (white = a object that stands out from background). Search points are generate by the *grid value*( gv=10, searches every 10% of the image).

**[multicrop2](http://www.fmwconcepts.com/imagemagick/multicrop2/index.php)** works by thresholding the image(making it black and white) then searches the **ENTIRE** image for white pixels (white = a object that stands out from background) Then discards all the objects that are smaller then the *discard value* you specified.

From my experience newspaper-multicrop2 tends to process faster.

### deskew vs textdeskew

**[deskew](https://www.imagemagick.org/script/command-line-options.php#deskew)**
is faster and is already built into ImageMagick.

**[textdeskew](http://www.fmwconcepts.com/imagemagick/textdeskew/index.php)**
is significantly slower but should yield better results. This is not built intro
imagemagick and requires additional configuration (*see step 4 of the installation*).
Sometimes `textdeskew` outputs images that are the wrong orientation.  From my experience
these images are still aligned, so after the script runs, a simple rotation of 90
degrees should do.
For more information on how `textdeskew` works read the
**[documentation on Fred Weinhaus's website](http://www.fmwconcepts.com/imagemagick/textdeskew/index.php)**.


<a name="myworkflow"></a>
# My Workflow
## 1. Scanning
To ensure the scripts perform optimally, follow these guidlines

*  Items stand out from background
*  Space in between items
*  Space between items and scanner borders
*  Relatively Straight orientation(for all items)

![bad-background-example](https://i.imgur.com/p0CZgWZ.jpg)

#### Flood Filling

*Image masks* are created quickly by technique called [Flood Filling](https://en.wikipedia.org/wiki/Flood_fill). Flood Fills start at a pixel then branch out taking over adjacent pixels that are the same color. They eat away at the background until they are stopped by an object that is not the background color.  See the animation below the *flood fill* will eat into the items

We will create an *image mask* in the next step.

![Imgur](https://i.imgur.com/kd3TGj8.gif)



[//]: # "As you can see in the animations above *flood fills* travel via the background color.  Therefore ample space bewteen each item is needed to properly fill the mask."
<a name="create-a-mask"></a>
## 2. Creating a mask
Masks indicate what parts of the image is a newspaper clippings and what part is the background.  Creating a mask can be done using Freds [multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php) script or A GUI program such as photoshop or gimp.  

*Freds script can be faster and works well when the newspaper clippings clearly stand out from the background. I tend to use a GUI program, for more precision*

#### With an GUI program
[How to create a mask in photoshop (link)](https://www.youtube.com/watch?v=GquHeiaNdxw&feature=youtu.be)

#### With Multicrop
```sh
$ mulitcrop -f 15 -p 5 -m output image.tif output-mask.gif
```
The flag values `-f 15` & `-p 5`  work for my test scans. Reading the documentation for [multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php) will help different cases


## 3.Running the scripts
Say you have `image.tif` that contains 5 news clipping

you've created a mask for it `image_mask.gif`

you've put both of this files in a folder `my-scans`

```
+---my-scans
    +--image.tif
    +--image_mask.gif
```

Running the following command in `my-scans` directory

```sh
$ newspaper-multicrop image.tif image_mask.gif 10 0
```
The script will do its thing and create a directory `image_cropped` to store all the crops

```
+---folder-of-stuff
    +--image.jpg
    +--image_mask.gif
    +--image_cropped
       +--image-00.png
       +--image-01.png
       +--image-02.png
       +--image-03.png
       +--image-04.png
```
<a name="disk-considerations"></a>

# Disk Considerations

**[multicrop](http://www.fmwconcepts.com/imagemagick/multicrop/index.php)**,
**[multicrop2](http://www.fmwconcepts.com/imagemagick/multicrop2/index.php)**,
and,
**[textdeskew](http://www.fmwconcepts.com/imagemagick/textdeskew/index.php)**
 write cache files to the disk.  For example a 600 dpi scan (6000x8000) resulted
  in around 1 gigabyte of cache files.  Therefore I would suggest running these
   scripts on a ram disk. Especially if your system only has a solid state drive,
    due to the limited write endurance of NAND based flash memory


<a name="what-exactly-the-script-does"></a>

# What the scripts does
1. Applys image mask to raw image creating a image with a transparent background
2. Executes Freds multicrop script with the transparent image
3. Deskews all the cropped images(result of freds multicrop script)
4. Converts the white background(left over from deroating) to transparent
5. Trims extra transparent border
