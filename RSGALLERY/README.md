# Image Gallery From A Directory Or Folder 
Creating a no-database PHP image gallery is as easy as getting a list of image files using `glob()` and outputting them in HTML.
```
 $images = glob("PATH/GALLERY/*.{jpg,jpeg,gif,png,bmp,webp}", GLOB_BRACE);
 foreach ($images as $i) { echo "<img src='gallery/". basename($i) ."'>"; }
```
## QUICK NOTES
- `gallery.php` – The simpler gallery without image caption.
- `caption-gallery.php` – Alternate version with image caption.
## STEP 1) PHP & HTML
![RimSam gallery](RSGALLERY/gallery/simple-gallery-1.webp)
