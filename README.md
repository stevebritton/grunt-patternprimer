# grunt-patternprimer v0.1.0 [![Build Status](https://travis-ci.org/asciidisco/grunt-patternprimer.png?branch=master)](https://travis-ci.org/asciidisco/grunt-patternprimer) [![devDependency Status](https://david-dm.org/stevebritton/grunt-patternprimer/dev-status.png?theme=shields.io)](https://david-dm.org/stevebritton/grunt-patternprimer#info=devDependencies)

> Grunt enabled port of [adactios](https://github.com/adactio) [Pattern-Primer](https://github.com/adactio/Pattern-Primer)



## What?!
As stated in the original docs:
> Create little snippets of markup and save them to the "patterns folder." The pattern primer will generate a list of all the patterns in that folder. You will see the pattern rendered as HTML. You will also get the source displayed in a textarea.

Check also the related [Blog Post](http://adactio.com/journal/5028/) & [example](http://patternprimer.adactio.com/) from Jeremy.

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-patternprimer --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-patternprimer');
```

## Patternprimer task
_Run this task with the `grunt patternprimer` command._

Task targets, files and options may be specified according to the grunt [Configuring tasks](http://gruntjs.com/configuring-tasks) guide.

### Options

#### wwwroot
Type: `String`  
Default: `public`

This is the Place all your HTML extracts (the pattern files) live it is relative to the  `<root>` folder of your project.

#### css
Type: `Array`  
Default: `['global.css']`

Array with all the css files you that should be loaded in the parttern primer.

#### dest
Type: `String`  
Default: `docs`

Specifies the destination of the pattern files when running a snapshot build and/or running the live server.

#### ports
Type: `Array`  
Default: `[7020, 7030]`

Ports that should be used when running the live server. The first index of that array will be used to serve the contents of the
`patterns` folder live, the second port will be used to serve your last snapshot build (if one exists).

#### src
Type: `String`
Default: `public/patterns`

The location of your pattern catalogue, this source will be used to deliver the pattern catalogue from the live server
and to generate snapshots from it.

#### snapshot
Type: `Boolean`  
Default: `false`

Determines if a live server should be fired up, or if the output ends up in the via `dest` configured snapshot directory.

#### index
Type: `Boolean` `String`
Default: `false`

Define your own index template for the patterns. Should be a file ending with the `.html` extension.
Please omit the closing `</body>` and `</html>` tags, they will be added autmagically.

### Usage examples

#### Live delivery

This configuration will start a live server that servers your pattern catalogue on port 7020.

```js
// Project configuration.
grunt.initConfig({
  patternprimer: {
    my_target: {
      ports: [7020],
      src: 'public/patterns',
      wwwroot: 'public',
      css: ['global.css']      
    }
  }
});
```

#### Creating snapshots

This configuration will not spin a live server, instead will save your catalogue (for static access)
in the `dest` folder:

```js
// Project configuration.
grunt.initConfig({
  patternprimer: {
    my_target: {
      wwwroot: 'public',
      css: ['global.css'],
      dest: 'docs',
      snapshot: true
    }
  }
});
```

#### Getting it all together

This configuration (my favourite) will enable you to run a live server & do snapshotting by specifying
the task from the cmd.

`grunt patternprimer:live` will spin up the servers to deliver the live catalogue & the last snapshotted version.

`grunt patternprimer:snapshot` will generate and save a new snapshot.
 
```js
// Project configuration.
grunt.initConfig({
  patternprimer: {
    options: {
      wwwroot: 'public',
      css: ['global.css'],
      dest: 'docs'
    },
    live: {
      ports: [7020, 7030],
      src: 'public/patterns',
    },
    snapshot: {
      snapshot: true
    }
  }
});
```

## Release History
 * 2013-11-25   v0.1.0   Initial release.
