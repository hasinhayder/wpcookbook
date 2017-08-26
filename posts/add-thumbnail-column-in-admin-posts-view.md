# Add a thumbnail column in all posts admin view 

You can easily add extra columns to the all posts table inside WordPress admin panel and fill it up with different kind of data. All you have to do is just filters like these

```php
add_filter('manage_posts_columns', 'wpcookbook_thumbnail_column', 10);

function wpcookbook_thumbnail_column($columns) {
	$columns['thumb'] = __('Featured Image','pacific');
	return $columns;
}

add_action('manage_posts_custom_column', 'wpcookbook_thumbnail_column_data', 10, 2);

function wpcookbook_thumbnail_column_data($column_name, $post_id) {
	if ($column_name == 'thumb') {
		echo get_the_post_thumbnail($post_id,"thumbnail");
	}
}
```

If you want to display a smaller image without adding an extra image-size, you can do it like this

```php
add_action('manage_posts_custom_column', 'wpcookbook_thumbnail_column_data', 10, 2);

function wpcookbook_thumbnail_column_data($column_name, $post_id) {
	if ($column_name == 'thumb') {
		echo get_the_post_thumbnail($post_id,array(75,75));
	}
}

```

The column you just added will display at the end. If you want to place it in a specific position, you can do so by rewriting `wpcookbook_thumbnail_column` like this

```php
function wpcookbook_thumbnail_column($columns) {
	$columns = array(
		'cb' => '<input type="checkbox" />',
		'thumb' => 'Thumbnail',
		'title' => 'Title',
		'author' => 'Author',
		'categories' => 'Categories',
		'tags' => 'Tags',
		'date' => 'Date',
	);
	$columns['thumb'] = __('Featured Image','pacific');
	return $columns;
}
```

Enjoy!

