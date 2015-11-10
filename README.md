# [gulp](http://gulpjs.com)-purge-sourcemaps
> Cleans up after gulp-sourcemaps have done a sourcemaps.write() allowing you to combine streams that generate both dev assets with sourcemaps and minified production assets.

## Install

```
npm install --save-dev gulp-purge-sourcemaps
```

## Example

```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var rename = require('gulp-rename');
var minifyCSS = require('gulp-minify-css');
var sourcemaps = require('gulp-sourcemaps');
var purgeSourcemaps = require('gulp-purge-sourcemaps');

gulp.task('default', function () {
  gulp.src('app.scss')
    .pipe(sourcemaps.init())
    .pipe(sass())
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('dist'))
    .pipe(purgeSourcemaps(/* sourcemaps.write() has been called, minifyCSS should not be fooled into thinking it's not generated yet */))
    .pipe(minifyCSS({keepSpecialComments:0, processImport: false}))
    .pipe(rename({suffix: '.min'}))
    .pipe(gulp.dest('dist'));
});
```

## License

MIT
