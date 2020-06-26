# Demo Gulp PostCSS Autoprefixer

Demo of:

* [Gulp](https://gulpjs.com/) tool to automate & enhance your workflow

* [PostCSS](https://postcss.org/) tool for transforming CSS with JavaScript

* [Autoprefixer](https://github.com/postcss/autoprefixer) plugin to parse CSS and add vendor prefixes to CSS rules 


## Setup


### Create a Node project

Create the directory:

```sh
mkdir demo
cd demo
```

Initiatlize git and add typical git ignore rules for any Node softare:

```sh
git init
curl https://github.com/github/gitignore/blob/master/Node.gitignore -o .gitignore
```

Initialize Node Package Manager (NPM), which handles package installation, version management, and dependency management:

```sh
npm init -y
```


### Add Gulp build system

Install Gulp, which is a build system that automates tasks for website development:

```sh
npm install --global gulp-cli
npm install --save-dev gulp
```

Verify:

```sh
gulp --version
```

```sh
CLI version: 2.3.0
Local version: 4.0.2
```

If gulp says "command not found", then try this [help](https://gist.github.com/rcugut/46904124d198a9dbd430abe88ebf849b)


### Create gulpfile

Create a text file `gulpfile.js`:

```js
var gulp = require('gulp');

gulp.task('default', async function() {
    console.log("gulp is running");
});
```

Run:

```sh
gulp
```

```sh
… Using gulpfile …/gulpfile.js
… Starting 'default'...
gulp default is working
… Finished 'default' after 2.63 ms
```


### Add gulp-postcss

Install:

```sh
npm install gulp-postcss --save-dev
```

Edit `gulpfile.js`:

```js
var gulp = require('gulp');
var postcss = require('gulp-postcss');

gulp.task('postcss', async function() {
    var plugin = [
        // PostCSS plugins will go here
    ];
    return gulp.src('./*.css')
        .pipe(postcss(plugin))
        .pipe(gulp.dest('./dest'));
});
```

Create a CSS file such as `styles.css`:

```css
h1 { font-color: red; }
```

Run:

```sh
gulp postcss
```

```sh
Using gulpfile …/gulpfile.js
… Starting 'postcss'...
… Finished 'postcss' after 19 ms
You did not set any plugins, parser, or stringifier. Right now, PostCSS does nothing. …
```

Verify results:

```sh
ls dest
```

```sh
output.css
styles.css
```


### Add any PostCSS plugin

Install any PostCSS plugin, such as autoprefixer:

```sh
npm install autoprefixer --save-dev
```

Edit `gulpfile.js`:

```js
var gulp = require('gulp');
var postcss = require('gulp-postcss');
var autoprefixer = require('autoprefixer');

gulp.task('postcss', async function() {
    var plugin = [
        autoprefixer()
    ];
    return gulp.src('./*.css')
        .pipe(postcss(plugin))
        .pipe(gulp.dest('./dest'));
});
```

Edit `styles.css` and try a setting that will use autoprefix:

```css
:fullscreen a {
    display: flex;
}
```

Run:

```sh
gulp postcss
```

Verify results:

```sh
cat dest/styles.css
```

```css
:-webkit-full-screen a {
    display: flex;
}
:-ms-fullscreen a {
    display: flex;
}
:fullscreen a {
    display: flex;
}
```
