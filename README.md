# gulp-include-require
Simple CommonJS style require() by including file.

## pros
* simple.
* support source-maps

## cons
* can only include from static string file name.
* if required multiple times, all require will be replaced by file contents.

## usage

```
npm install --save-dev file:/path/to/gulp-include-require
```

and in `gulpfile.js`

```
var includeRequire = require("gulp-include-require");

gulp.src("./src/*.js")
    .pipe(sourcemaps.init())
    .pipe(includeRequire())
    .pipe(sourcemaps.write())
    .pipe(gulp.dest("./dist"));
```

## example

```src/moduleA.js
module.exports = function( value ){
    return value*2;
}
```

```src/moduleB.js
var multiplyBy2 = require('./moduleA');
var result = multiplyBy2( 4 );
```

after this gulp plugin.

```dist/result.js
var multiplyBy2 = var config = (function(){
  var module = {};
  var exports = {};
  module.exports = function( value ){
      return value*2;
  }

  return module.exports || exports;
})() ;
var result = multiplyBy2( 4 );
```

----
[README from original gulp-include](./README-gulp-include.md)
