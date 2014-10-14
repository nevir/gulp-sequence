gulp-sequence v0.2.0 [![Build Status](https://travis-ci.org/teambition/gulp-sequence.svg)](https://travis-ci.org/teambition/gulp-sequence)
====
> Run a series of gulp tasks in order.

## Install

Install with [npm](https://npmjs.org/package/gulp-sequence)

```
npm install --save-dev gulp-sequence
```


## Usage

```js
var gulp = require('gulp'),
  gulpSequence = require('gulp-sequence');

gulp.task('a', function (cb) {
  //... cb()
});

gulp.task('b', function (cb) {
  //... cb()
});

gulp.task('c', function (cb) {
  //... cb()
});

gulp.task('d', function (cb) {
  //... cb()
});

gulp.task('e', function (cb) {
  //... cb()
});

gulp.task('f', function () {
  // return stream
  return gulp.src('*.js');
});

// usage 1, recommend
// 1. run 'a', 'b' in parallel;
// 2. run 'c' after 'a' and 'b';
// 3. run 'd', 'e' in parallel after 'c';
// 3. run 'f' after 'd' and 'e'.
gulp.task('sequence-1', gulpSequence(['a', 'b'], 'c', ['d', 'e'], 'f'));

// usage 2
gulp.task('sequence-2', function (cb) {
  gulpSequence(['a', 'b'], 'c', ['d', 'e'], 'f', cb);
});

// usage 3
gulp.task('sequence-3', function (cb) {
  gulpSequence(['a', 'b'], 'c', ['d', 'e'], 'f')(cb);
});

gulp.task('gulp-sequence', gulpSequence('sequence-1', 'sequence-2', 'sequence-3'));
```

## API

```js
var gulpSequence = require('gulp-sequence');
```

### gulpSequence('subtask1', 'subtask2',...[, callback])
return [thunk](https://github.com/teambition/thunks) function.

### gulpSequence.use(gulp)
return gulpSequence. Use the effective gulp.

## License

MIT © [Teambition](http://teambition.com)
