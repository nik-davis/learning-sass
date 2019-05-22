1. Install nodejs and npm package manager

https://nodejs.org/en/download/

2. Globally install sass

```
npm install -g node-sass
```

3. Create styles.scss file

```
$padding: 6px;

nav {
  ul {
    margin: 0;
    padding: $padding;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: $padding 12px;
    text-decoration: none;
  }
}
```

4. Create tasks.json (Terminal > configure tasks > create tasks.json file from template > others)

```
// Sass configuration
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Sass Compile",
            "type": "shell",
            "command": "node-sass styles.scss styles.css",
            "group": "build"
        }
    ]
}
```

5. Run build task (Ctrl+Shift+B), should create styles.css

6. For automation, install gulp

```
npm install -g gulp
npm install gulp gulp-sass
gulp -v
```

Should see version for both global (CLI) and local

7. Create gulpfile.js at root

```
// Sass configuration
var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function(cb) {
    gulp.src('*.scss')
        .pipe(sass())
        .pipe(gulp.dest(function(f) {
            return f.base;
        }));
    cb();
});

gulp.task('default', gulp.series('sass', function(cb) {
    gulp.watch('*.scss', gulp.series('sass'));
    cb();
}));
```

8. Delete tasks.json or empty, Run Task and pick gulp:default

9. Finally, terminate from global Terminal menu
