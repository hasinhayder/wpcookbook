# Enqueue last modified version of scripts and css files

WordPress sites are often displayed with cached version of css and javascript files. That is good, until you modify something and want your users to see the latest changes on their browsers. Users keep seeing older versions as long as the cache is not expired or until they explicitely clear their browser cache. Now that is a problem which you can deal with a nice workaround, called cachebuster. 

People often use the common `time()` function to pass as version number while enquing script. This is a good technique for debugging scripts, but bad for live sites because it creates a new cached version of the script on user's browser everytime they visit or refresh the site. 

So we will use the last modified time as version number. This will dynamically change everytime you modify a css or javascript file and ensure that last modified file gets loaded without much efforts. 

```php
add_action( "wp_enqueue_scripts", "wpcookbook_include_js_and_css" );

function wpcookbook_include_js_and_css() {
	wp_enqueue_script(
		"wpcbjs",
		get_template_directory_uri() . "/scripts/main.js",
		"jquery",
		filemtime(get_template_directory()."/scripts/main.js"),
		true
	);
}
```

Neat, eh?