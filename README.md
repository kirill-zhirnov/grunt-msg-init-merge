# grunt-msg-init-merge

> Grunt task for msginit and msgmerge

## Getting Started
This plugin requires Grunt `~0.4.5`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-msg-init-merge --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-msg-init-merge');
```

## The "msgInitMerge" task

### Overview
This task runs for each locale:
* **msginit** if **.po** file does not exist to create it.
* **msgmerge** if **.po** file exists to update it with new keywords.

In your project's Gruntfile, add a section named `msgInitMerge` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  msgInitMerge: {
    your_target: {
      options: {
          locales: [{name: 'ru_RU', folder: 'ru'}, 'en'],
          poFilesPath: 'tmp/i18n/<%= locale%>/<%= potFileName%>.po',
      },
      src: ['test/fixtures/myDomain.pot']
    }
  },
});
```

You should specify:
* **locales** - list of locales
* **poFilesPath** -  template for *.po files location.
* **src** - location of *.pot files.

Task in example above will create/update *.po files:
* tmp/i18n/ru/myDomain.po
* tmp/i18n/en/myDomain.po

### Options

#### options.locales
Type: `Array`

Default value: []

List of locales:
```js
[{name: 'ru_RU', folder: 'ru'}, 'en']
```

If locale is an Object:
* name - will be passed to msginit --locale=name
* folder - will be used as locale variable in poFilesPath template (folder name).

#### options.poFilesPath
Type: `String`

Default value: `''`

Template for *.po files location:
```js
tmp/i18n/<%= locale%>/<%= potFileName%>.po
```
Available variables:
* locale - locale folder
* potFileName - name of a *.pot file

#### options.msgInit
Type: `Object`

Default value: ```js
msgInit : {
    cmd : 'msginit',
    opts : {}
}
```

You can specify path to msginit or additional options:
```js
msgInit : {
    cmd : '/opt/local/bin/msginit',
    opts : {
        width : 50
    }
}
```
#### options.msgMerge
Type: `Object`

Default value: ```js
msgMerge : {
    cmd : 'msgmerge',
    opts : {}
}
```

You can specify path to msgmerge or additional options:
```js
msgMerge : {
    cmd : '/opt/local/bin/msgmerge',
    opts : {
        width : 50
    }
}
```