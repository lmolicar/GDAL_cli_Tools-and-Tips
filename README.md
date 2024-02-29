# GDAL_cli_Tools-and-Tips

## Clipping rasters with polygons using GDAL

Source [link](https://web.archive.org/web/20160602133713/http://linfiniti.com:80/2009/09/clipping-rasters-with-gdal-using-polygons/).

This is a useful example of how:
* determine the extent of your clipmask
* perform a rectangular clip on the image
* perform a polygonal clip on the image

But note that when getting the extent of the clipmask, I had to modify the awk call. Here's my code for comparison:

```bash
EXTENT=`$ogrinfoExec -al -so $SHPFILE| grep Extent \
| sed 's/Extent: //g' | sed 's/(//g' | sed 's/)//g' \
| sed 's/ - /, /g'`
EXTENT=`echo $EXTENT | gawk 'BEGIN {FS=","}; {printf "%f %f %f %f", $1, $4, $3, $2}'`
echo $EXTENT
```
