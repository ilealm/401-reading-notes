[ HOME ](README.md)
# Read - Getting Stylish with Sass

## django-sass-processor

- Refer SASS/SCSS files directly from your sources, instead of referring a compiled CSS file, having to rely on another utility which creates them from SASS/SCSS files, hidden in your source tree.
- Use Django's settings.py for the configuration of paths, box sizes etc., instead of having another SCSS specific file (typically _variables.scss), to hold these.
- Extend your SASS functions by calling Python functions directly out of your Django project.
-  View SCSS errors directly in the debug console of your Django's development server.


django-sass-processor converts *.scss or *.sass files into *.css while rendering templates. For performance reasons this is done only once, since the preprocessor keeps track on the timestamps and only recompiles, if any of the imported SASS/SCSS files is younger than the corresponding generated CSS file.

This Django app provides a templatetag, which can be used instead of the built-in templatetag static. This templatetag also works inside Jinja2 templates.

If SASS/SCSS files shall be referenced through the Media class, or media property, the SASS processor can be used directly.

Additionally, django-sass-processor is shipped with a management command, which can convert the content of all occurrences inside the templatetag sass_src as an offline operation. Hence the libsass compiler is not required in a production environment.

During development, a sourcemap is generated along side with the compiled *.css file. This allows to debug style sheet errors much easier.

With this tool, you can safely remove your Ruby installations "Compass" and "SASS" from your Django projects. You neither need any directory "watching" daemons based on node.js.



**_Installation_**

`pip install libsass django-compressor django-sass-processor`


**_Configuration_**
In settings.py add to:

```
import os

SASS_PROCESSOR_INCLUDE_DIRS = [
    os.path.join(PROJECT_PATH, 'extra-styles/scss'),
    os.path.join(PROJECT_PATH, 'node_modules'),
]

INSTALLED_APPS = [
    ...
    'sass_processor',
    ...
]

STATICFILES_FINDERS = [
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',
    'sass_processor.finders.CssFinder',
    ...
]

SASS_PROCESSOR_AUTO_INCLUDE = False

SASS_PROCESSOR_INCLUDE_FILE_PATTERN = r'^.+\.scss$'

TEMPLATES = [{
    'BACKEND': 'django.template.backends.jinja2.Jinja2',
    'DIRS': [],
    'APP_DIRS': True,
    'OPTIONS': {
        'environment': 'yourapp.jinja2.environment'
    },
    ...
}]

```

**_Usage_**

In your Django templates
{% load sass_tags %}

`<link href="{% sass_src 'myapp/css/mystyle.scss' %}" rel="stylesheet" type="text/css" />`

## Configure SASS variables through settings.py

In SASS, a nasty problem is to set the correct include paths for icons and fonts. Normally this is done through a _variables.scss file, but this inhibits a configuration through your projects settings.py.

To avoid the need for duplicate configuration settings, django-sass-processor offers a SASS function to fetch any arbitrary configuration directive from the project's settings.py. This is specially handy to set the include path of your Glyphicons font directory. Assume, Bootstrap-SASS has been installed using:

`npm install bootstrap-sass`

then locate the directory named node_modules and add it to your settings, so that your fonts are accessible through the Django's django.contrib.staticfiles.finders.FileSystemFinder:

```
STATICFILES_DIRS = [
    ...
    ('node_modules', '/path/to/your/project/node_modules/'),
    ...
]

NODE_MODULES_URL = STATIC_URL + 'node_modules/'
```

# Sass Basics

CSS on its own can be fun, but stylesheets are getting larger, more complex, and harder to maintain. This is where a preprocessor can help. Sass lets you use features that don't exist in CSS yet like variables, nesting, mixins, inheritance and other nifty goodies that make writing CSS fun again.

Once you start tinkering with Sass, it will take your preprocessed Sass file and save it as a normal CSS file that you can use in your website.

The most direct way to make this happen is in your terminal. Once Sass is installed, you can compile your Sass to CSS using the sass command. You'll need to tell Sass which file to build from, and where to output CSS to. For example, running sass input.scss output.css from your terminal would take a single Sass file, input.scss, and compile that file to output.css.

You can also watch individual files or directories with the --watch flag. The watch flag tells Sass to watch your source files for changes, and re-compile CSS each time you save your Sass. If you wanted to watch (instead of manually build) your input.scss file, you'd just add the watch flag to your command, like so:

`sass --watch input.scss output.css`

You can watch and output to directories by using folder paths as your input and output, and separating them with a colon. In this example:

`sass --watch app/sass:public/stylesheets`

Sass would watch all files in the app/sass folder for changes, and compile CSS to the public/stylesheets folder.

## Variables

```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## Nesting

Sass will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. Be aware that overly nested rules will result in over-qualified CSS that could prove hard to maintain and is generally considered bad practice.

```
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

## Partials
You can create partial Sass files that contain little snippets of CSS that you can include in other Sass files. This is a great way to modularize your CSS and help keep things easier to maintain. A partial is a Sass file named with a leading underscore. You might name it something like _partial.scss. The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@use rule`.

## Modules

ou don't have to write all your Sass in a single file. You can split it up however you want with the @use rule. This rule loads another Sass file as a module, which means you can refer to its variables, mixins, and functions in your Sass file with a namespace based on the filename. 

```
// _base.scss
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}


// styles.scss
@use 'base';

.inverse {
  background-color: base.$primary-color;
  color: white;
}
```

## Mixins
Some things in CSS are a bit tedious to write, especially with CSS3 and the many vendor prefixes that exist. A mixin lets you make groups of CSS declarations that you want to reuse throughout your site. You can even pass in values to make your mixin more flexible. A good use of a mixin is for vendor prefixes. 

```
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box { @include transform(rotate(30deg)); }
```

## Extend/Inheritance
This is one of the most useful features of Sass. Using @extend lets you share a set of CSS properties from one selector to another. It helps keep your Sass very DRY. In our example we're going to create a simple series of messaging for errors, warnings and successes using another feature which goes hand in hand with extend, placeholder classes. A placeholder class is a special type of class that only prints when it is extended, and can help keep your compiled CSS neat and clean.

```
/* This CSS will print because %message-shared is extended. */
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

// This CSS won't print because %equal-heights is never extended.
%equal-heights {
  display: flex;
  flex-wrap: wrap;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

## Operators
Doing math in your CSS is very helpful. Sass has a handful of standard math operators like +, -, *, /, and %. In our example we're going to do some simple math to calculate widths for an aside & article.

```
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}
```


# Sources
[django-sass-processor](https://github.com/jrief/django-sass-processor#introduction)

[Sass Basics](https://sass-lang.com/guide)
