URL replacement for HTML Webpack Plugin
=======================================

[![Build Status](https://travis-ci.com/BTOdell/replace-url-html-webpack-plugin.svg?branch=master)](https://travis-ci.com/BTOdell/replace-url-html-webpack-plugin)
![npm](https://img.shields.io/npm/v/replace-url-html-webpack-plugin.svg)
![npm dependencies](https://david-dm.org/btodell/replace-url-html-webpack-plugin.svg)
![node](https://img.shields.io/node/v/replace-url-html-webpack-plugin.svg)
![npm type definitions](https://img.shields.io/npm/types/replace-url-html-webpack-plugin.svg)
![npm license](https://img.shields.io/npm/l/replace-url-html-webpack-plugin.svg)

[![NPM](https://nodei.co/npm/replace-url-html-webpack-plugin.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/replace-url-html-webpack-plugin/)

This is an extension plugin for the [webpack](https://www.npmjs.com/package/webpack) plugin [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin) - a plugin that simplifies the creation of HTML files to serve your webpack bundles.

Typically, [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin) injects `<script>` and `<link>` elements into generated HTML.
When used with a template, [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin) will still inject new elements regardless of whether or not elements already exist for the assets.

This plugin will automatically update the URLs for existing `<script>` and `<link>` elements in an HTML template with URLs generated by Webpack.
It identifies existing elements by comparing their URLs with the generated output file name from Webpack. See Example section.

Webpack doesn't handle CSS resources natively.
However, by using some of the following plugin combinations you can make them accessible to [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin):
* copy-webpack-plugin ([npm](https://www.npmjs.com/package/copy-webpack-plugin)) ([github](https://github.com/webpack-contrib/copy-webpack-plugin)),<br>
html-webpack-include-assets-plugin ([npm](https://www.npmjs.com/package/html-webpack-include-assets-plugin)) ([github](https://github.com/jharris4/html-webpack-include-assets-plugin))
* extract-text-webpack-plugin ([npm](https://www.npmjs.com/package/extract-text-webpack-plugin)) ([github](https://github.com/webpack-contrib/extract-text-webpack-plugin)) (warning: untested)

Environment
-----------
* [node](https://nodejs.org/) >= 6.11.5

Peer Dependencies
------------
* webpack ([npm](https://www.npmjs.com/package/webpack)) ([github](https://github.com/webpack/webpack)) >= 4.0.0
* html-webpack-plugin ([npm](https://www.npmjs.com/package/html-webpack-plugin)) ([github](https://github.com/jantimon/html-webpack-plugin)) >= 4.0.0

Installation
------------
Install the plugin as a development dependency using npm:
```shell
$ npm install replace-url-html-webpack-plugin --save-dev
```

Basic Usage
-----------

The plugin has no configuration. Simply, add the plugin to your webpack config as follows:

```javascript
{
  plugins: [
    new HtmlWebpackPlugin(),
    new ReplaceUrlHtmlWebpackPlugin()
  ]
}
```

The order is important - the plugin must come **after** HtmlWebpackPlugin.

Example
-------

Consider the following HTML template:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>Example</title>
        <link type="text/css" rel="stylesheet" href="css/index.css" />
        <script async="async" src="js/bundle.js"></script>
    </head>
    <body>
        ...
    </body>
</html>
```

If webpack is configured to generate the bundle with a hash included, then the URLs for both `<script>` and `<link>` will be replaced:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>Example</title>
        <link type="text/css" rel="stylesheet" href="css/index.abcdef0123456789.css" />
        <script async="async" src="js/bundle.abcdef0123456789.js"></script>
    </head>
    <body>
        ...
    </body>
</html>
```
