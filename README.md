# csr - Compass Sprites Retina

## About

csr mixin is a basic solution for creating retina sprites using SASS and Compass.
csr mixin contain also csr-base helper mixin, which is used to show how to make custom helper mixin for csr, or to extend it in custom helper mixin.

## The problem

You want your site to serve retina images to retina displays, but not to non-retina ones. This mixin / solution will make it very easy for you to use sprites and let Compass generate the mappings of the two different sizes.

Since we have to develop sites that serve retina images and background-images our sprites and background-image approaches might get a bit cluttered in our CSS. Using just one call, this mixin will know which image has to be served to the browser and will also resize it to show as if it was in your normal image dimentions.

## How to use

First you need to download csr mixin (_csr.scss) to your project mixins directory and import it before file where you want to use it.

### Basic usage

1. Put social network icons into
  ```
  | images/
  |-- icons/
      |-- social/
          |-- facebook.png
          |-- facebook-2x.png
          |-- twitter.png
          |-- twitter-2x.png
          |-- google-plus.png
          |-- google-plus-2x.png
  ```

2. Create Compass map variable with the name of your sprite, and pass needed arguments.<br> 
  Example:
  
  SCSS:
  ```scss
  ///
  /// Social networks icons sprite.
  ///
  $social-icons: sprite-map("icons/social/*.png", $spacing: 20px, $sort-by: width) !default;
  ```
  
  *First time when you call csr mixin with `$social-icons` map, sprite image will be generated into*
  ```
  | images/
  |-- generated/
      |-- icons/
          |-- social-[attached_with_some_string].png
  ```

3. Create your helper mixin which you will use later with `$social-icons` sprite map variable.
  Example:
  
  SCSS:
  ```scss
  ///
  /// Social icons sprite.
  /// @param {String} $file-name - Icon file name.
  /// @param {Object} $options - Optional object options.
  /// @see {mixin} csr-base
  ///
  @mixin social-icon($file-name, $options: ()) {
    @include csr-base($social-icons, $file-name, $options);
  }
  ```

4. Style link with background image from sprite.
  Example:
  
  SCSS:
  ```scss
  .social-icons {
    a[href*="facebook"] {@include social-icon('facebook');
  }
  ```
  
  HTML
  ```html
  <ul class="social-icons">
    <li><a href="http://facebook.com/">Facebook</a></li>
  <ul>
  ```
  