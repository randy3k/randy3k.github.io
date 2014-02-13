---
layout: post
published: true
title: Wordpress Categories Filter
tagline: ''
category: 'computing'
tags: [wordpress, php]
---

This is how wordpress filters out some specific categories. You may need to change the category id.
<!--more-->
{% highlight php %}
<?php
/*
Plugin Name: My Filter
*/

// Exit if accessed directly
if ( !defined('ABSPATH')) exit;

# to exclude the category testing
function exclude_category($query) {
if ($query->is_search) {
$query->set('cat', '-3');
}
return $query;
}
add_filter('pre_get_posts', 'exclude_category');

function exclude_widget_categories($args) {
$exclude = "3"; // The IDs of the excluding categories
$args["exclude"] = $exclude;
return $args;
}

add_filter("widget_categories_args","exclude_widget_categories");

function myFilter($query) {
if ($query->is_home) {
$query->set('cat','-3');
}
return $query;
}
add_filter('pre_get_posts','myFilter');

function exclude_stuff($query) {
if ( $query->is_date) {
$query->set('cat', '-3');
}
return $query;
}
add_filter('pre_get_posts', 'exclude_stuff');

add_filter( 'getarchives_where', 'customarchives_where' );
add_filter( 'getarchives_join', 'customarchives_join' );

function customarchives_join( $x ) {
global $wpdb;
return $x . " INNER JOIN $wpdb->term_relationships ON ($wpdb->posts.ID = $wpdb->term_relationships.object_id) INNER JOIN $wpdb->term_taxonomy ON ($wpdb->term_relationships.term_taxonomy_id = $wpdb->term_taxonomy.term_taxonomy_id)";
}

function customarchives_where( $x ) {
global $wpdb;
$exclude = '3'; // category id to exclude
return $x . " AND $wpdb->term_taxonomy.taxonomy = 'category' AND $wpdb->term_taxonomy.term_id NOT IN ($exclude)";
}

?>
{% endhighlight %}