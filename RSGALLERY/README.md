 #   <img src="gallery/rimsam.png" width="50px" height="50px" alt="RimSam">Image Gallery From A Directory Or Folder 
>
>
Creating a no-database PHP image gallery is as easy as getting a list of image files using `glob()` and outputting them in HTML.
```
 $images = glob("PATH/GALLERY/*.{jpg,jpeg,gif,png,bmp,webp}", GLOB_BRACE);
 foreach ($images as $i) { echo "<img src='gallery/". basename($i) ."'>"; }
```

##  <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam">QUICK NOTES
- `gallery.php` – The simpler gallery without image caption.
- `caption-gallery.php` – Alternate version with image caption.

##  <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam">STEP 1) PHP & HTML
![RimSam gallery](gallery/simple-gallery-1.webp)
> gallery.php
```
<!-- (A) CSS & JS -->
<link href="gallery.css" rel="stylesheet">
<script src="gallery.js"></script>
<div class="gallery"><?php
$dir = __DIR__ . DIRECTORY_SEPARATOR . "gallery" . DIRECTORY_SEPARATOR;
$images = glob("$dir*.{jpg,jpeg,gif,png,bmp,webp}", GLOB_BRACE); 
foreach ($images as $i) {
  printf("<img src='gallery/%s'/>", basename($i));
}
?></div>
```
Yep, that’s all to the gallery page. As in the introduction, all we are doing here is –
- Get a list of image files from the gallery folder using `glob()`.
- Then throw them into the `<div class="gallery">` gallery container.
##  <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam">STEP 2) THE CSS
> gallery.css
```
.gallery {
  display: grid;
  grid-template-columns: repeat(3, auto);
  grid-gap: 10px;
  max-width: 1200px;
  margin: 0 auto;
}
@media screen and (max-width: 640px) {
  .gallery {
    grid-template-columns: repeat(2, auto);
  }
}
.gallery img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}
.gallery img:fullscreen { object-fit: contain; }
body, html {
  padding: 0;
  margin: 0;
}
```
Of course, we are not so “barbaric” to just row out raw images without any cosmetics. So here is how we use a simple CSS grid to layout the images into a nice gallery, also add some responsive mobile-friendly magic. Please feel free to modify these to fit your own project.
##  <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam">STEP 3) JAVASCRIPT FULLSCREEN IMAGE
> gallery.js
```
window.addEventListener("DOMContentLoaded", () => {
  var all = document.querySelectorAll(".gallery img");
  if (all.length>0) { for (let img of all) {
    img.onclick = () => {
      if (document.webkitFullscreenElement || document.fullscreenElement) {
        if (document.exitFullscreen) { document.exitFullscreen(); }
        else if (document.webkitExitFullscreen) { document.webkitExitFullscreen(); }
      }
      else {
        if (img.requestFullscreen) { img.requestFullscreen(); }
        else if (img.webkitRequestFullscreen) { img.webkitRequestFullscreen(); }
      }
    });
  }}
});
```
Lastly, a small Javascript snippet to “click on an image to toggle fullscreen mode”.

##  <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam"> EXTRA) FILENAME AS IMAGE CAPTION
> caption-gallery.php
```
foreach ($images as $i) {
  $img = basename($i);
  $caption = substr($img, 0, strrpos($img, "."));
  printf("<figure><img src='gallery/%s'/><figcaption>%s</figcaption></figure>", $img, $caption);
}
```
Since there is no database, there is nowhere we can store the captions. But we can still use the file name as the caption of the images – This is just a small modification to the PHP to also output the `<figcaption>`.

  #### <img src="gallery/rimsam.png" width="15px" height="15px" alt="RimSam"> If you spot a bug, feel free to comment below. I try to answer short questions too, but it is one person versus the entire world… If you need answers urgently, please check out [Get Help](https://github.com/samsermolla).

