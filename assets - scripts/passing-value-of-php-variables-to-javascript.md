# Passing value of PHP variables to JavaScript

This ay sound little weird, but the application is huge. I mean come on, there are many times you wanted to get the values of some PHP variables inside your JavaScript files. You don't need ajax or any complex mime-format directives for your web server to do it for you. WordPress gives an easy way to get this job done, all you have to do is use the `wp_localize_script` function. 

```php
<?php

add_action( "wp_enqueue_scripts", "wpcookbook_include_js_and_css" );

function wpcookbook_include_js_and_css() {
	global $wp_version;
	$data = array( "version" => $wp_version, "admin_ajaxurl" => admin_url( "admin-ajax.php" ) );
	wp_enqueue_script( "wpcbjs", get_template_directory_uri() . "/scripts/main.js", "jquery", "1.0", true );
	wp_localize_script( "wpcbjs", "simblog", $data );
}
```

Above code will pass a global variable called **jsvars** to your main.js file, which you can access like this

```js
;(function($){
    $(document).ready(function(){
        console.log(jsvars);
        alert(jsvars.version);
        alert(jsvars.admin_ajaxurl);
    });
})(jQuery);
```

If your JavaScript file had no dependency on jQuery, you could rewrite this code like 


```js
console.log(jsvars);
alert(jsvars.version);
alert(jsvars.admin_ajaxurl);
```

That is quite a lifesaver technique, eh?