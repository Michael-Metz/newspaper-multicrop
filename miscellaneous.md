# Miscellaneous Notes

### ImageMagick Notes
###### Floodfill white border and replace with transparent
```
convert -bordercolor white -border 1x1 -alpha set -channel RGBA -fuzz 1% -fill none -floodfill +0+0 white -shave 1x1 [infile] [outfile]
```
###### Crop out extra transparent border pixels
```
convert -bordercolor none -border 10x10 -trim +repage [infile] [outfile]

```
