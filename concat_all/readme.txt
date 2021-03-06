=== concat_all ===
Contributors: majidfouladpour
Tags: minify, script, style, concatenate
Requires at least: 3.4
Tested up to: 4.5.3
Stable tag: trunk
License: MIT
License URI: https://opensource.org/licenses/MIT

This plugin will concatenate and cache all css and js code in the output of your site.

== Description ==

This is the list of changes the plugin makes:  

* Buffers output for the following processing
* Finds all script elements (of type "text/javascript", with or without `src`)
* Uses a hash of either the `src` or the content of the script block to create a cache filename
* Checks if the cache file has already been created. If so, it proceeds to concatenating css
* Grabs the js source from in-file script blocks as well as external files
* Concatenates all js and saves to cache directory, preserving the same order the originals appeared in output
* Does the same with `link rel='stylesheet'` and `style` elements and if cached file does not exist, creates it.
* Removes the now redundant *script*, *link*, and *style* elements from HTML source
* Adds a single *link* element to *head* and a single *script* element before *body* closes for the cached resources
* Minifies the HTML source and sends the output

== Installation ==
1. If \'wp-content/uploads\' directory is not writable, manually add a \'wp-content/uploads/concat_all_cache\' directory and make it writable.
2. Place concat_all directory under your wp-content/plugins directory.
3. In your Adin panel under Plugins, find and enable 'Concat All' plugin.

== Frequently Asked Questions ==

= Why not minify CSS and JS? =
We are not minifying css and js when we concatenate them. There are several reasons for this:

* It is the responsibility of each plugin or template author to minify js and css for production
* Many resources are already minified, but have no clue in the file name so we might attempt minification of minified source
* Often source files include a copyright block in the form of comments that are stripped during minification, which is bad, because you are supposed to preserve those notices

If, however, you see that resulting cahced css and js would shrink significantly if all sources are minified, do the minification on the source files. There are comments above each block that show where the original resource was taken from.


= Are there any known issues? =

* The plugin uses output buffering, which might interfere with setups/plugins that cannot have their output buffered. In such cases, the plugin cannot be used.

* If you have `<pre>`, `<code>` or filled `<textarea>` elements in your output, newlines and other whitespace will not be preserved while minifying the HTML. If this is the case, comment out the line that minifiys the output prior to sending it, or, change the minifier code to not remove whitespace within those elements!

== Changelog ==

= 0.2 =
In this version hard-coded paths where replaced by getting the path from `wp_upload_dir()` function.

== Upgrade Notice ==

= 0.2 =
Upgrade advised.

== Misc. ==

The plugin would not work without output buffering and the code for that has been taken verbatim from [this SO answer](http://stackoverflow.com/a/22818089/66580), thanks [@kfriend](http://stackoverflow.com/users/419673/kfriend).
For HTML minification I am using the `minify_html` function from [this gist](https://gist.github.com/tovic/d7b310dea3b33e4732c0), thanks [@Taufik Nurrohman](https://github.com/tovic).

The source code is also available on Github: https://github.com/majid4466/concat_all

Copyright © 2016 Majid Fouladpour | MIT license
