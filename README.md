# gulp-check-unused-css

Check if all your defined CSS classes are used in your HTML files.

## Usage
    
    var checkCSS = require( 'gulp-check-unused-css' );
    gulp
        .src( 'allmy.css' )
        .pipe( checkCSS({
            files: 'templates/*.html'
        }))
        .on( 'error', function( err ) {
            // unnecessary since gulp-check-unused-css logs by default
            console.log( 'Unused classes:', err.unused );
        });

If there are no unused classes it will just output your CSS file for later usage, e.g. minifying.

In case you don't want an error event, but instead the stream to end, use the ``end`` flag. This is especially useful when used together with ``gulp-watch`` since an error will trip it up. It will not fail, but also stop working correctly.

    watch({ glob: 'allmy.css' })
        .pipe( checkCSS({
            end: true,
            files: 'templates/*.html'
        }))
        .pipe( whatever )
        .pipe( gulp.dest(... ) );

## Ignoring classes

Sometimes you style classes in your CSS that are not explicitly used in your templates. Either you inlined the HTML in your code (*ewww*) or maybe they are generated by a framework you use, e.g. AngularJS. That's where you want to exclude classes from being checked.

### By Name

You can provide a list of class names that should be ignored.

    gulp
        .src( 'my.css' )
        .pipe( checkCSS({
            files: 'templates/*.html',
            ignoreClassNames: [ 'ignore-me', 'me-too' ]
        }))
        .pipe( gulp.dest( ... ) );

### By Pattern

Alternatively (or additionally) you can provide a list of patterns that a class name must not match in order to be checked.

    gulp
        .src( 'my.css' )
        .pipe( checkCSS({
            files: 'templates/*.html',
            ignoreClassPatterns: [ /ignore*/gi, /me-?too/ ]
        }))
        .pipe( gulp.dest( ... ) );


## Development

    git clone gulp-check-unused-css
    cd gulp-check-unused-css
    npm install
    # hack hack hack
    npm test
