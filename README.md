## Climate data processing
This is the documenation for the AR5 climate data processing. Most of the work was done with the R package called raster, and with Python and gdal using the osgeo4w toolset

## Converting to GeoTiff
A python script was used to pluck out the years we wanted from the netcdf and then convert them to GeoTiff. The end result was geotiff files in full time-series from 2020-2039, 2040-2059, 2060-2079, and 2080-2099. 

[Code for Iterating through many files and rotating them](https://github.com/deriggi/AR5-World-Bank/blob/master/rotateAll.R)


### Rotating the files
Many climate models a longitudnal scale which runs from 0 -> 360 instead of the standard 0 -> -180. For these data sets we first had to rotate the data

The following image is an example of a raster that neeeds to be rotated. you will notice that you cannot simply shift the raster west because then the hemispheres would not align

![Alt text](images/rotation.png)

[Code for Iterating through many files and rotating them](https://github.com/deriggi/AR5-World-Bank/blob/master/rotateAll.R)

### Stacking the rasters

The next step involved is stacking the rasters. Instead of having separate rasters for each year, we can us R to stack them up for easier processing. This is basically an exercise using R's stack function in the raster package. We simply grab a chuck that are of the same model, sort them, and then stack them. We have to be very careful that we are sorting them correctly!

[Code for stacking rasters](https://github.com/deriggi/AR5-World-Bank/blob/master/rasterStacker.R)

### Monthly averages

We want to show the monthly averages for each 20 year period rather than the time-series data because it is more informative. To do that we must average each month within our raster stacks.

We create a raster stack of all the January months, average the stack, write the output, and then move on to the next month.

[Code for stacking rasters](https://github.com/deriggi/AR5-World-Bank/blob/master/monthTrender.R)








