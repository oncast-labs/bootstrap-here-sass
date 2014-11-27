# Bootstrap (here) for Sass

`bootstrap-here-sass` is a Sass-powered version of [Bootstrap](http://github.com/twbs/bootstrap), modified to affect only elements within an outer element with attribute `data-bootstrap-here`

All selectors are prefixed (or sufixed in case of html or body elements) with selector [data-bootstrap-here]

For more information about bootstrap-sass, take a look in [bootstrap-sass-official](http://github.com/twbs/bootstrap-sass)

## Installation

* [Bower](#c-bower).

### a. Bower

Since bootstrap-sass is still being tested with bower, this also is still being tested :-/. bootstrap-sass is compatible with node-sass 0.8.3+. You can install it with:

```console
$ bower install --save bootstrap-here-sass
```

`bootstrap-sass` is taken so make sure you use the command above.

Sass, JS, and all other assets are located at [assets](/assets).

By default, `bower.json` main field list only the main `bootstrap.scss` and all the static assets (fonts and JS).
This is compatible by default with asset managers such as [wiredep](https://github.com/taptapship/wiredep).

### Configuration

#### Sass

By default all of Bootstrap is imported.

You can also import components explicitly. To start with a full list of modules copy
[`_bootstrap.scss`](assets/stylesheets/_bootstrap.scss) file into your assets as `_bootstrap-custom.scss`.
Then comment out components you do not want from `_bootstrap-custom`.
In the application Sass file, replace `@import 'bootstrap'` with:

```scss
@import 'bootstrap-custom';
```

#### Sass: Number Precision

bootstrap-sass [requires](https://github.com/twbs/bootstrap-sass/issues/409) minimum [Sass number precision][sass-precision] of 10 (default is 5).

Precision is set for Rails and Compass automatically.
When using ruby Sass compiler standalone or with the Bower version you can set it with:

```ruby
::Sass::Script::Number.precision = [10, ::Sass::Script::Number.precision].max
```

Note that libsass and node-sass do not currently support the precision option, due to an open bug ([bug #364](https://github.com/sass/libsass/issues/364)) in libsass.


#### Sass: Autoprefixer

Using [Autoprefixer][autoprefixer] with Bootstrap is recommended.
[Autoprefixer][autoprefixer] adds vendor prefixes to CSS rules using values from [Can I Use](http://caniuse.com/).

#### JavaScript

[`assets/javascripts/bootstrap.js`](/assets/javascripts/bootstrap.js) contains all of Bootstrap JavaScript,
concatenated in the [correct order](/assets/javascripts/bootstrap-sprockets.js).


#### JavaScript with Sprockets or Mincer

If you use Sprockets or Mincer, you can require `bootstrap-sprockets` instead to load the individual modules:

```js
// Load all Bootstrap JavaScript
//= require bootstrap-sprockets
```

You can also load individual modules, provided you also require any dependencies.
You can check dependencies in the [Bootstrap JS documentation][jsdocs].

```js
//= require bootstrap/scrollspy
//= require bootstrap/modal
//= require bootstrap/dropdown
```

#### Fonts

The fonts are referenced as:

```scss
"#{$icon-font-path}#{$icon-font-name}.eot"
```

`$icon-font-path` defaults to `bootstrap/` if asset path helpers are used, and `../fonts/bootstrap/` otherwise.

When using bootstrap-sass with Compass, Sprockets, or Mincer, you **must** import the relevant path helpers before Bootstrap itself, for example:

```scss
@import "bootstrap-compass";
@import "bootstrap";
```

## Usage

### Sass

Import Bootstrap into a Sass file (for example, application.css.scss) to get all of Bootstrap's styles, mixins and variables!

```scss
@import "bootstrap";
```

You can also include optional bootstrap theme:

```scss
@import "bootstrap/theme";
```

The full list of bootstrap variables can be found [here](http://getbootstrap.com/customize/#less-variables). You can override these by simply redefining the variable before the `@import` directive, e.g.:

```scss
$navbar-default-bg: #312312;
$light-orange: #ff8c00;
$navbar-default-color: $light-orange;

@import "bootstrap";
```

## Version

`bootstrap-sass` version reflects the upstream version, with an additional number for Sass-specific changes.

Always refer to [CHANGELOG.md](/CHANGELOG.md) when upgrading.

---

## Development and Contributing

If you'd like to help with the development of bootstrap-sass itself, read this section.

### Upstream Converter

Keeping bootstrap-sass in sync with upstream changes from Bootstrap used to be an error prone and time consuming manual process. With Bootstrap 3 we have introduced a converter that automates this.

**Note: if you're just looking to *use* Bootstrap 3, see the [installation](#installation) section above.**

Upstream changes to the Bootstrap project can now be pulled in using the `convert` rake task.

Here's an example run that would pull down the master branch from the main [twbs/bootstrap](https://github.com/twbs/bootstrap) repo:

    rake convert

This will convert the latest LESS to Sass and update to the latest JS.
To convert a specific branch or version, pass the branch name or the commit hash as the first task argument:

    rake convert[e8a1df5f060bf7e6631554648e0abde150aedbe4]

The latest converter script is located [here][converter] and does the following:

* Converts upstream bootstrap LESS files to its matching SCSS file.
* Copies all upstream JavaScript into `assets/javascripts/bootstrap`, an Sprockets manifest at `assets/javascripts/bootstrap-sprockets.js`, and a concatenation at `assets/javascripts/bootstrap.js`.
* Copies all upstream font files into `assets/fonts/bootstrap`.
* Sets `Bootstrap::BOOTSTRAP_SHA` in [version.rb][version] to the branch sha.

This converter fully converts original LESS to SCSS. Conversion is automatic but requires instructions for certain transformations (see converter output).
Please submit GitHub issues tagged with `conversion`.

## Credits

bootstrap-sass has a number of major contributors:

<!-- feel free to make these link wherever you wish -->
* [Thomas McDonald](https://twitter.com/thomasmcdonald_)
* [Tristan Harward](http://www.trisweb.com)
* Peter Gumeson
* [Gleb Mazovetskiy](https://github.com/glebm)

and a [significant number of other contributors][contrib].

## You're in good company
bootstrap-sass is used to build some awesome projects all over the web, including
[Diaspora](http://diasporaproject.org/), [rails_admin](https://github.com/sferik/rails_admin),
Michael Hartl's [Rails Tutorial](http://railstutorial.org/), [gitlabhq](http://gitlabhq.com/) and
[kandan](http://kandanapp.com/).

[converter]: https://github.com/twbs/bootstrap-sass/blob/master/tasks/converter/less_conversion.rb
[version]: https://github.com/twbs/bootstrap-sass/blob/master/lib/bootstrap-sass/version.rb
[contrib]: https://github.com/twbs/bootstrap-sass/graphs/contributors
[antirequire]: https://github.com/twbs/bootstrap-sass/issues/79#issuecomment-4428595
[jsdocs]: http://getbootstrap.com/javascript/#transitions
[sass-precision]: http://sass-lang.com/documentation/Sass/Script/Number.html#precision-class_method
[mincer]: https://github.com/nodeca/mincer
[autoprefixer]: https://github.com/ai/autoprefixer
