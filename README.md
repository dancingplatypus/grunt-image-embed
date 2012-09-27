This project was forked from Eric Hynds's grunt-image-embed (git://github.com/ehynds/grunt-image-embed.git), who did all the
heavy lifting. This task converts all images found within a stylesheet (those within a `url( ... )` declaration) into base64-encoded data URI strings.

This is probably a faux pas, and I'll write Eric, but I needed something that would encode multiple URL's on the same
line, which his version did not do.  I needed this because the LESS compiler does exactly that when compiling my
font-face declarations.

## Features

* Supports both local & remote images.
* Ability to specify a size limit. Default is 32kb, or IE8's limit.
* Existing data URIs will be ignored.
* Skip specific images by specifying a directive comment.
* Includes two helpers: `encode_stylesheet` to encode a stylesheet, and `encode_image` to encode an image.

## Getting Started

Install this plugin with: `grunt install dancingplatypus-grunt-image-embed`

Next, add this line to your project's `grunt.js` file:

`grunt.loadNpmTasks("grunt-image-embed");`

Lastly, add the configuration settings to your grunt.js file.

## Documentation

This task has two required properties, `src` and `dest`. `src` is the path to your stylesheet and `dest` is the file this task will write to (relative to the grunt.js file). If this file already exists **it will be overwritten**.

An example configuration looks like this:

```` javascript
grunt.initConfig({
  imageEmbed: {
    dist: {
      src: [ "css/styles.css" ],
      dest: "css/output.css"
    }
  }
});
````

### Optional Configuration Properties

ImageEmbed can be customized by specifying the following options:

* `maxImageSize`: The maximum size of the base64 string in bytes. This defaults to `32768`, or IE8's limit. Set this to `0` to remove the limit and allow any size string.
* `baseDir`: If you have absolute image paths in your stylesheet, the path specified in this option will be used as the base directory.
* `deleteAfterEncoding`: remove the original image after encoding.  Probably don't want to do this if you are deploying right out of your source directory.

### Skipping Images

Specify that an image should be skipped by adding the following comment *after* the image, before any other punctuation:

`background: url(image.gif)/*ImageEmbed:skip*/`

## License

Copyright (c) 2012 Michael Hays and contributors
Licensed under the MIT License.
