# Miscellaneous Notes

### ImageMagick Notes
#### Floodfill white border and replace with transparent
```
convert -bordercolor white -border 1x1 -alpha set -channel RGBA -fuzz 1% -fill none -floodfill +0+0 white -shave 1x1 [infile] [outfile]
```
#### Crop out extra transparent border pixels
```
convert -bordercolor none -border 10x10 -trim +repage [infile] [outfile]

or

mogrify -bordercolor none -border 10x10 -trim +repage *.png
```
#### Split an image 
[https://unix.stackexchange.com/questions/169534/how-to-split-an-image-vertically-using-the-comand-line](https://unix.stackexchange.com/questions/169534/how-to-split-an-image-vertically-using-the-comand-line)


## Resize all images in current directory to 300dpi. (Careful this will overwrite the original file)

```
for file in *;  do convert -resample 300 "$file" "$file"; done
```

## run multicrop on a folder of zeropadded images with masks

consider the following folder structure

```
+raw
+--00.jpg
+--00_mask.png
+--01.jpg
+--01_mask.png
+--02.jpg
+--02_mask.png
+--03.jpg
+--03_mask.png
   ...
   ...
   ...
+--99.jpg
+--99_mask.png
```

This script below will run `newspaper-multicrop2` on all the `image/mask` pairs in the raw folder

```sh
numDigits=2
counter=$((0));
for file in *.jpg;do
  formatString="%0$numDigits"
  d="d"
  formatString="$formatString$d"
  printf -v number "$formatString" $counter
  
  newspaper-multicrop2 "$number".jpg "$number"_mask.png 200 0
  counter=$((counter+1))
done
```
