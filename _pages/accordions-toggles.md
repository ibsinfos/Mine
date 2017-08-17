---
ID: 2712
post_title: 'Accordions &#038; Toggles'
author: admin
post_excerpt: ""
layout: page
permalink: >
  http://criptocoin.wordpress-experts.net/shortcodes-2/accordions-toggles/
published: true
post_date: 2014-05-15 06:34:44
---
<h3 class="widget-title">Accordion Code</h3>
[container padding="10px 0"][title size="small" align="center" &lt;?php
/*
Plugin Name: Templatemela Shortcodes
Plugin URI: http://www.templatemela.com
Description: Templatemela Custom Shortcodes for templatemela wordpress themes.
Version: 1.0
Author: Templatemela
Author URI: http://www.templatemela.com
*/

/***************** accordion ****************/

function shortcode_accordion($atts, $content = null) {

extract(shortcode_atts(array(
'style'    =&gt; '1'
), $atts));

$output = '';
$output .= '&lt;div class="accordion style'.$style.'"&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_accordion', 'shortcode_accordion');

function shortcode_single_accordion($atts, $content = null)
{
extract(shortcode_atts(array(
'title' =&gt; 'Click here to hide/show Div'
), $atts));
$output = '';
$output .= '&lt;div class="single_accordion"&gt;';
$output .= '&lt;a class="tog" href="#"&gt;&lt;div class="accordion-title"&gt;&lt;span class="icon"&gt;&lt;/span&gt;'.$title.'&lt;/div&gt;&lt;/a&gt;';
$output .= '&lt;div class="tab_content"&gt;'.do_shortcode($content).'&lt;/div&gt;';
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('accordion', 'shortcode_single_accordion');


/******************************Newsletter*******************************/
function shortcode_newsletter_text($atts, $content = null){
extract(shortcode_atts(array(
'text1' =&gt; '',
'text2' =&gt; '',
'description' =&gt; '',
), $atts));
$output = '';
$output .= '&lt;div class="newslettercontainer"&gt;';
$output .= '&lt;div class="newslettercontainerinner"&gt;';
$output .= '&lt;div class="border-top"&gt; &lt;/div&gt;';
if(!empty($text1))
$output .= '&lt;h1 class="simple-type small-title"&gt;'.$text1.'&lt;/h1&gt;';
if(!empty($text2))
$output .= '&lt;div class="text2"&gt;'.$text2.'&lt;/div&gt;';
if(!empty($description))
$output .= '&lt;div class="description"&gt;'.$description.'&lt;/div&gt;';
$output .= '&lt;div class="newsletter-text-content"&gt;';
$output .=  do_shortcode($content);
$output .= '&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('newsletter_text', 'shortcode_newsletter_text');

/***************** Toggle ****************/
function shortcode_toggle($atts, $content = null) {

extract(shortcode_atts(array(
'style'    =&gt; '1'
), $atts));

$output = '';
$output .= '&lt;div class="toggle style'.$style.'"&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_toggle', 'shortcode_toggle');

function shortcode_single_toggle($atts, $content = null)
{
extract(shortcode_atts(array(
'title' =&gt; 'Click here to hide/show Div'
), $atts));
$output = '';
$output .= '&lt;div class="single_toggle toogle_div"&gt;';
$output .= '&lt;a class="tog" href="#"&gt;&lt;div class="toggle-title"&gt;&lt;span class="icon"&gt;&lt;/span&gt;'.$title.'&lt;/div&gt;&lt;/a&gt;';
$output .= '&lt;div class="tab_content"&gt;'.do_shortcode($content).'&lt;/div&gt;';
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('toggle', 'shortcode_single_toggle');

/***************** Horizontal Tab ****************/

$maintab_div = '';

function tabs_group($atts, $content = null ) {
global $maintab_div;
extract(shortcode_atts(array(
'tab_type' =&gt; 'horizontal',
'style'    =&gt; '1'
), $atts));

switch ($tab_type) {
case 'vertical' :
$element_class = 'vertical_tab';
break;
default :
$element_class = 'horizontal_tab';
break;
break;
}


$maintab_div = '';
$output = '&lt;div id="'.$element_class.'" class="'.$element_class.' style'.$style.'"&gt;&lt;div id="tab" class="tab"&gt;&lt;ul class="tabs"&gt;';
$output.= do_shortcode($content).'&lt;/ul&gt;';
$output.= '&lt;div class="tab_groupcontent"&gt;'.$maintab_div.'&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_tabs', 'tabs_group');

function tab($atts, $content = null) {
global $maintab_div;

static $oddeven_class=0;
$oddeven_class++;
$newclass = '';
$output = '';
if($oddeven_class % 2 == 0) { $newclass .= "even"; } else  { $newclass .= "odd"; }

extract(shortcode_atts(array(
'title' =&gt; '',
), $atts));
$dummy_title = "'. __( 'Tab', 'templatemela' ) .'";

if($title != NULL) {
$output .= '&lt;li class="'.$newclass.'"&gt;&lt;a href="#"&gt;'.$title.'&lt;span class="leftarrow"&gt;&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;';
} else {
$output .= '&lt;li class="'.$newclass.'"&gt;&lt;a href="#"&gt;'.$dummy_title.'&lt;span class="leftarrow"&gt;&lt;/span&gt;&lt;/a&gt;&lt;/li&gt;';
}
$maintab_div.= '&lt;div class="tabs_tab"&gt;'.$content.'&lt;/div&gt;';
return $output;
}
add_shortcode('tm_tab', 'tab');

/***************** Testimonial ****************/
function shortcode_testimonials($atts, $content = null, $code) {
extract(shortcode_atts(array(
'style' =&gt; '1',
'type' =&gt; 'grid',
'items_per_column' =&gt; 3,
'number_of_posts' =&gt; 5,
'image_width' =&gt; 50,
'image_height' =&gt; 50,
'background_color' =&gt; 'F7F7F7'
), $atts));

global $post;
$i = 1;
$args = array(
'posts_per_page' =&gt; $number_of_posts,
'post_status' =&gt; 'publish',
'post_type' =&gt; 'testimonial',
);
$testimonial_array = get_posts($args);
$testimonial_count = count($testimonial_array);
$output = '';
if($testimonial_count &gt; 0 ):
$output .= '&lt;div class="testimonials-container main-ul"&gt;';
if($type == "slider") {
if($testimonial_count &gt; $items_per_column)
$output .= '&lt;div id="'.$items_per_column.'_testimonial_carousel" class="testimonial-carousel"&gt;';
else
$output .= '&lt;div id="testimonial_grid" class="testimonial-grid testimonial-cols-'.$items_per_column.'"&gt;';
} else if($type == "grid") {
$output .= '&lt;div id="testimonial_grid" class="testimonial-grid testimonial-cols-'.$items_per_column.'"&gt;';
} else if($type == "list") {
$output .= '&lt;div id="testimonial_list" class="testimonial-list"&gt;';
}
$i = 1;
foreach($testimonial_array as $post) : setup_postdata($post);
get_post_meta($post-&gt;ID, 'testimonial_position', TRUE) ? $testimonial_position = get_post_meta($post-&gt;ID, 'testimonial_position', TRUE) : $testimonial_position = '';
get_post_meta($post-&gt;ID, 'testimonial_link', TRUE) ? $testimonial_link = get_post_meta($post-&gt;ID, 'testimonial_link', TRUE) : $testimonial_link = '';
$contents = strip_tags(templatemela_strip_images($post-&gt;post_content));
if($i % $items_per_column == 1)
$class = " first-item";
elseif($i % $items_per_column == 0)
$class = " last-item";
else
$class = "";
$output .= '&lt;div class="item'.$class.'"&gt;&lt;div class="product-block"&gt;';
$output .= '&lt;div class="single-testimonial"&gt;';
$output .= '&lt;div class="testimonial-content"&gt;';
$output .= '&lt;div class="testimonial-top" style="'.$background_color.'"&gt;&lt;blockquote&gt;&lt;q&gt;'.substr($contents, 0, 150).'&lt;/q&gt;&lt;/blockquote&gt;&lt;/div&gt;';
$output .= '&lt;div class="testimonial-bottom"&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="testmonial-other"&gt;';
$output .= '&lt;div class="testmonial-image"&gt;';
if ( has_post_thumbnail() &amp;&amp; ! post_password_required() ) :
$post_thumbnail_id = get_post_thumbnail_id();
$post_thumbnail_url = wp_get_attachment_url( $post_thumbnail_id );
$output .= '&lt;img src="'.mr_image_resize($post_thumbnail_url, $image_width, $image_height, true, 'center', false).'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
else:
$output .= '&lt;i style="width:'.$image_width.';height:'.$image_height.';" class="fa fa-user"&gt;&lt;/i&gt;';
endif;
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="testmonial-text"&gt;';
$output .= '&lt;div class="testimonial-title"&gt;'.get_the_title().'&lt;/div&gt;';
if(!empty($testimonial_position)):
if(!empty($testimonial_link)):
$output .= '&lt;div class="testimonial-email"&gt;&lt;a target="_Blank" title="'.$testimonial_position.'" href="'.$testimonial_link.'" &gt;'.$testimonial_position.'&lt;/a&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="testimonial-email"&gt;'.$testimonial_position.'&lt;/div&gt;';
endif;
endif;
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
$i++;
endforeach;
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
else:
$output .= '&lt;div class="no-result"&gt;No results found...&lt;/div&gt;';
endif;
wp_reset_query();
return $output;
}
add_shortcode('tm_testimonials', 'shortcode_testimonials');

/***************** Our Team ****************/
function shortcode_ourteam($atts, $content = null) {
extract(shortcode_atts(array(
'type' =&gt; 'grid',
'items_per_column' =&gt; 4,
'number_of_posts' =&gt; -1
), $atts));

global $post;
$i = 1;
$output = '';
wp_reset_postdata();
$args = array(
'posts_per_page' =&gt; $number_of_posts,
'post_status' =&gt; 'publish',
'post_type' =&gt; 'staff',
'orderby' =&gt; 'date'
);

$output = '';
$team_array = new WP_Query( $args );

if ( $team_array-&gt;have_posts() ):
$output .= '&lt;div id="team-posts-products" class="team-posts-content staff-page posts-content"&gt;';
if($type == "slider") {
$output .= '&lt;div id="'.$items_per_column.'_team_carousel" class="team-carousel"&gt;';
} else {
$output .= '&lt;div id="team_grid" class="team-grid grid cols-'.$items_per_column.'"&gt;';
}

while ( $team_array-&gt;have_posts() ) : $team_array-&gt;the_post();
get_post_meta(get_the_ID(), 'staff_position', TRUE) ? $staff_position = get_post_meta(get_the_ID(), 'staff_position', TRUE) : $staff_position = '';
get_post_meta(get_the_ID(), 'staff_link', TRUE) ? $staff_link = get_post_meta(get_the_ID(), 'staff_link', TRUE) : $staff_link = '';
get_post_meta(get_the_ID(), 'staff_phone', TRUE) ? $staff_phone = get_post_meta(get_the_ID(), 'staff_phone', TRUE) : $staff_phone = '';
get_post_meta(get_the_ID(), 'staff_email', TRUE) ? $staff_email = get_post_meta(get_the_ID(), 'staff_email', TRUE) : $staff_email = '';
get_post_meta(get_the_ID(), 'staff_twitter', TRUE) ? $staff_twitter = get_post_meta(get_the_ID(), 'staff_twitter', TRUE) : $staff_twitter = '';
get_post_meta(get_the_ID(), 'staff_facebook', TRUE) ? $staff_facebook = get_post_meta(get_the_ID(), 'staff_facebook', TRUE) : $staff_facebook = '';
get_post_meta(get_the_ID(), 'staff_google_plus', TRUE) ? $staff_google_plus = get_post_meta(get_the_ID(), 'staff_google_plus', TRUE) : $staff_google_plus = '';
get_post_meta(get_the_ID(), 'staff_linkedin', TRUE) ? $staff_linkedin = get_post_meta(get_the_ID(), 'staff_linkedin', TRUE) : $staff_linkedin = '';
get_post_meta(get_the_ID(), 'staff_youtube', TRUE) ? $staff_youtube = get_post_meta(get_the_ID(), 'staff_youtube', TRUE) : $staff_youtube = '';
get_post_meta(get_the_ID(), 'staff_rss', TRUE) ? $staff_rss = get_post_meta(get_the_ID(), 'staff_rss', TRUE) : $staff_rss = '';
get_post_meta(get_the_ID(), 'staff_pinterest', TRUE) ? $staff_pinterest = get_post_meta(get_the_ID(), 'staff_pinterest', TRUE) : $staff_pinterest = '';
get_post_meta(get_the_ID(), 'staff_skype', TRUE) ? $staff_skype = get_post_meta(get_the_ID(), 'staff_skype', TRUE) : $staff_skype = '';

$s = 0;
if(!empty($staff_link)) $s++;
if(!empty($staff_email)) $s++;
if(!empty($staff_twitter)) $s++;
if(!empty($staff_facebook)) $s++;
if(!empty($staff_google_plus)) $s++;
if(!empty($staff_linkedin)) $s++;
if(!empty($staff_youtube)) $s++;
if(!empty($staff_rss)) $s++;
if(!empty($staff_pinterest)) $s++;
if(!empty($staff_skype)) $s++;
if($i % $items_per_column == 1 )
$class = " first";
elseif($i % $items_per_column == 0 )
$class = " last";
else
$class = "";
if ( has_post_thumbnail() &amp;&amp; ! post_password_required() ) :
$post_thumbnail_id = get_post_thumbnail_id();
$image = wp_get_attachment_url( $post_thumbnail_id );
else:
$image = get_template_directory_uri()."/images/placeholders/placeholder.jpg";
endif;
$src = mr_image_resize($image, 600, 600, true, 't', false);
if( empty ( $src ) || $src == 'image_not_specified' ):
$src = get_template_directory_uri()."/images/megnor/placeholder.png";
$src = mr_image_resize($src, 600, 600, true, 't', false);
endif;
$output .= '&lt;article class="item container'.$class.'"&gt;';
$output .= '&lt;div class="single-team container-inner"&gt;';
$output .= '&lt;div class="staff-image"&gt;';
$output .= '&lt;img src="'.$src.'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="staff-content"&gt;';
$shorttitle = substr(the_title('','',FALSE),0,150);
$output .= '&lt;div class="team-content-box"&gt;';
$output .= '&lt;div class="staff-name"&gt;'.$shorttitle.'&lt;/div&gt;';
$output .= '&lt;div class="staff-position"&gt;&lt;span&gt;'.$staff_position.'&lt;/span&gt;&lt;/div&gt;';
$output .= '&lt;div class="staff-social icon-'.$s.'"&gt;';
if(!empty($staff_link) &amp;&amp; $staff_link != '')
$output .= '&lt;a href="'.$staff_link.'" title="Website" class="website icon"&gt;&lt;i class="fa fa-link"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_email) &amp;&amp; $staff_email != '')
$output .= '&lt;a href="mailto:'.$staff_email.'" title="Email" class="email icon"&gt;&lt;i class="fa fa-envelope-o"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_twitter) &amp;&amp; $staff_twitter != '')
$output .= '&lt;a href="'.$staff_twitter.'" title="Twitter" class="twitter icon"&gt;&lt;i class="fa fa-twitter"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_facebook) &amp;&amp; $staff_facebook != '')
$output .= '&lt;a href="'.$staff_facebook.'" title="Facebook" class="facebook icon"&gt;&lt;i class="fa fa-facebook"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_google_plus) &amp;&amp; $staff_google_plus != '')
$output .= '&lt;a href="'.$staff_google_plus.'" title="Google Plus" class="google-plus icon"&gt;&lt;i class="fa fa-google-plus"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_linkedin) &amp;&amp; $staff_linkedin != '')
$output .= '&lt;a href="'.$staff_linkedin.'" title="Linkedin" class="linkedin icon"&gt;&lt;i class="fa fa-linkedin"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_youtube) &amp;&amp; $staff_youtube != '')
$output .= '&lt;a href="'.$staff_youtube.'" title="Youtube" class="youtube icon"&gt;&lt;i class="fa fa-youtube"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_rss) &amp;&amp; $staff_rss != '')
$output .= '&lt;a href="'.$staff_rss.'" title="RSS" class="rss icon"&gt;&lt;i class="fa fa-rss"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_pinterest) &amp;&amp; $staff_pinterest != '')
$output .= '&lt;a href="'.$staff_pinterest.'" title="Pinterest" class="pinterest icon"&gt;&lt;i class="fa fa-pinterest"&gt;&lt;/i&gt;&lt;/a&gt;';
if(!empty($staff_skype) &amp;&amp; $staff_skype != '')
$output .= '&lt;a href="'.$staff_skype.'" title="Skype" class="skype icon"&gt;&lt;i class="fa fa-skype"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;&lt;/article&gt;';
$i++;
endwhile;
wp_reset_postdata();
$output .=    '&lt;/div&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="no-result"&gt;No results found...&lt;/div&gt;';
endif;
return $output;
}
add_shortcode("tm_ourteam", "shortcode_ourteam");

/***************** Pricing Table ****************/

function shortcode_pricingtable($atts, $content = null) {
extract(shortcode_atts(array(
"style" =&gt; '1',
"heading" =&gt; '',
"button_text" =&gt; '',
"button_link" =&gt; '',
"price" =&gt; '',
"price_per" =&gt; '',
"selected" =&gt; 'no',
), $atts));

if($selected == 'yes')
{
$selected = 'selected';
}
$output = '';
$output .='&lt;div class="pricing_wrapper"&gt;';
$output .='&lt;div class="pricing_wrapper_inner style-'.$style.' '.$selected.'"&gt;';
if($style == '1') {
if($heading != '' &amp;&amp; $price_per != '' &amp;&amp; $price != '') {
$output .='&lt;div class="pricing_heading"&gt;'.$heading.'&lt;/div&gt;';
$output .='&lt;div class="pricing_top"&gt;';
$output .='&lt;div class="pricing_per"&gt;'.$price_per.'&lt;/div&gt;';
$output .='&lt;div class="pricing_price"&gt;'.$price.'&lt;/div&gt;&lt;/div&gt;';
}
else{
$output .='&lt;div class="nopricing_heading"&gt;&lt;/div&gt;';
$output .='&lt;div class="nopricing_top"&gt;&lt;div class="pricing_per"&gt;&lt;/div&gt;&lt;div class="pricing_price"&gt;&lt;/div&gt;&lt;/div&gt;';
}
}
else
{
if($heading != '' &amp;&amp; $price_per != '' &amp;&amp; $price != '') {
$output .='&lt;div class="pricing_top"&gt;';
$output .='&lt;div class="pricing_heading"&gt;'.$heading.'&lt;/div&gt;';
$output .='&lt;div class="pricing_per"&gt;'.$price_per.'&lt;/div&gt;';
$output .='&lt;div class="pricing_price"&gt;'.$price.'&lt;/div&gt;&lt;/div&gt;';
}
else{
$output .='&lt;div class="nopricing_top"&gt;&lt;div class="nopricing_heading"&gt;&lt;/div&gt;';
$output .='&lt;div class="pricing_per"&gt;&lt;/div&gt;&lt;div class="pricing_price"&gt;&lt;/div&gt;&lt;/div&gt;';
}
}

$output .='&lt;div class="pricing_bottom"&gt;';
$output .='&lt;ul&gt;';
$output .= do_shortcode($content);
$output .='&lt;/ul&gt;';
$output .='&lt;div class="pricing_button"&gt;';
if($button_text != '') {
$output .='&lt;a href="'.$button_link.'" target="_blank" class="button" id="pricing-btn"&gt;'.$button_text .'&lt;/a&gt;';
}
$output .='&lt;/div&gt;&lt;/div&gt;';
$output .='&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode("tm_pricingtable", "shortcode_pricingtable");

function shortcode_pricingtable_row($atts, $content = null)
{
extract(shortcode_atts(array(
"symbol" =&gt; '',
), $atts));
$output = '';
if(!empty($symbol))
$output .= '&lt;li&gt;&lt;i class="fa '.$symbol.'"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;/li&gt;';
else
$output .= '&lt;li&gt;'.do_shortcode($content).'&lt;/li&gt;';
return $output;
}
add_shortcode('price_row', 'shortcode_pricingtable_row');

/***************** List Style ****************/

function shortcode_list($atts, $content = null)
{
extract(shortcode_atts(array(
'icon' =&gt;  'fa-circle-o',
'color' =&gt; '696868',
), $atts));
$output = '';
$output .= '&lt;li&gt;&lt;i style="color:#'.$color.'" class="fa '.$icon.'"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;/li&gt;';
return $output;
}
add_shortcode('list_item', 'shortcode_list');

function shortcode_tm_list($atts, $content = null)
{
extract(shortcode_atts(array(
), $atts));
$output = '';
$output .= '&lt;ul class="list"&gt;';
$output .= do_shortcode($content);
$output .=    '&lt;/ul&gt;';
return $output;
}
add_shortcode('tm_list', 'shortcode_tm_list');

/***************** Icon ****************/

function theme_shortcode_icon($atts, $content = null) {
extract(shortcode_atts(array(
'icon' =&gt; 'fa-users',
'color' =&gt; '212121',
), $atts));

return '&lt;span class="icon_text"&gt;&lt;i style="color:#'.$color.'" class="fa '.$icon.'"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;/span&gt;';
}
add_shortcode('tm_icon', 'theme_shortcode_icon');

/***************** Divider Space and Gap ****************/

function shortcode_divider($atts, $content = null) {
extract(shortcode_atts(array(
'type' =&gt; '',
'space' =&gt; ''
), $atts));

$elem_value = '';
switch ($type) {
case 'dotted' :
$elem_value = 'dotted';
break;
case 'dashed' :
$elem_value = 'dashed';
break;
case 'double' :
$elem_value = 'double';
break;
case 'groove' :
$elem_value = 'groove';
break;
case 'solid' :
$elem_value = 'solid';
break;
default :
$elem_value = '';
break;
break;
}

if($space != NULL) { $space = 'height:'.$space.';' ; } else { $space = '';    }

$output =    '&lt;div class="divider_content"&gt;';
$output .=    '&lt;div class="divider_content_inner divider_element"&gt;&lt;p&gt;';
$output .=    do_shortcode($content).'&lt;/p&gt;';
$output .=    '&lt;div class="'.$elem_value.'" style="'.$space.'"&gt;&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_divider', 'shortcode_divider');

/***************** Call to Action Area Button ****************/
function shortcode_calltoaction($atts, $content = null)
{
extract(shortcode_atts(array(
'link_title' =&gt; '',
'link_url' =&gt; '',
'animation_type' =&gt; 'fadeInLeft',
'sub_description' =&gt; '',
'align' =&gt; 'left',
'color' =&gt; '',
'button_color' =&gt; '',
'button_background_color' =&gt; '',
'button_background_hover_color' =&gt; ''
), $atts));

$output = '';
$output .= '&lt;div class="calloutarea '.$align.'"&gt;';
$output .= '&lt;div class="calloutarea_block animated" data-animated="'.$animation_type.'" style="color: #'.$color.'" &gt;';
$output .= '&lt;div class="calloutarea_block_content"&gt;';
if($align == 'center')
$output .= '&lt;h2 class="title" style="color: #'.$color.'"&gt;'.do_shortcode($content).'&lt;/h2&gt;';
else
$output .= '&lt;h3 class="title" style="color: #'.$color.'"&gt;'.do_shortcode($content).'&lt;/h3&gt;';
if(!empty($sub_description))
$output .= '&lt;div class="shortcode_content"&gt;'.$sub_description.'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
if(!empty($link_title))
$output .= '&lt;div class="calloutarea_button"&gt;&lt;a href="'.$link_url.'" class="button" style="color: '.$button_color.' onMouseOver="this.style.backgroundColor='."#".$button_background_color.'" onMouseOut="this.style.backgroundColor='."#".$button_background_hover_color.'"&gt;'.$link_title.'&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_calltoaction', 'shortcode_calltoaction');

/***************** Highlight Text ****************/
function shortcode_highlight($atts, $content = null) {
extract(shortcode_atts(array(
'style' =&gt; 'light'

), $atts));
$output = '';
$output .= '&lt;span class="hightlight_text highlight_'.$style . '"&gt;' . do_shortcode($content) . '&lt;/span&gt;';
return $output;
}
add_shortcode('tm_highlighttext', 'shortcode_highlight');


/***************** DropCap Text ****************/
function shortcode_dropcaps($atts, $content = null, $code) {
extract(shortcode_atts(array(
'color' =&gt; 'FFFFFF',
'background_color' =&gt; '282828',
'text_transform' =&gt; 'uppercase'
), $atts));

if(empty($background_color))
$class = " no-background";
else
$class = "";

$output = '';
$output .= '&lt;span class="dropcap'.$class.'" style="color:#'.$color.'; background-color:#'.$background_color.';text-transform:'.$text_transform.'"&gt;' . do_shortcode($content) . '&lt;/span&gt;';
return $output;
}
add_shortcode('tm_dropcap', 'shortcode_dropcaps');


/***************** Benefits ****************/
function shortcode_benefits($atts, $content = null)
{
extract(shortcode_atts(array(
'benefits_style' =&gt; 'column3',
'benefits_img' =&gt; '',
'benefits_name' =&gt; 'Responsive Design',
'benefits_linktitle' =&gt; 'View detail',
'benefits_urllink' =&gt; '#',
), $atts));

switch ($benefits_style) {
case 'style2' :
$col_width = 'column2';
break;
case 'style3' :
$col_width = 'column1';
break;
default :
$col_width = 'column3';
break;
break;
}

if($benefits_img != NULL) {
$get_imagepath = get_template_directory_uri() . '/images/megnor/' . $benefits_img;
} else {
$get_imagepath = get_template_directory_uri() . '/images/megnor/no_image.jpg';
}
$output = '';
$output .='&lt;div class="benefitsarea '.$col_width.'"&gt;';
$output .= '&lt;div class="benefitsarea_inner"&gt;';
$output .='&lt;div class="benifit_image"&gt;';
$output .= '&lt;span class="benefit_bkg animated" data-animated="bounceIn"&gt;&lt;img src="'.$get_imagepath.'" alt="benifit_image" /&gt;&lt;/span&gt;&lt;/div&gt;';
$output .= '&lt;div class="benefitsarea_bottom"&gt;&lt;div class="benifit_name"&gt;'. $benefits_name.'&lt;/div&gt;';
$output .= '&lt;p&gt;'.do_shortcode($content).'&lt;/p&gt;';
$output .= '&lt;div class="viewmore"&gt;&lt;a href="'.$benefits_urllink.'" target="_blank"&gt;'.$benefits_linktitle.' &lt;i class="fa fa-angle-double-right"&gt;&lt;/i&gt;&lt;/a&gt;&lt;/div&gt;';
$output .=    '&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_benefits', 'shortcode_benefits');

/***************** Blockquote  ****************/
function shortcode_quote($atts, $content = null)
{
extract(shortcode_atts(array(
'style' =&gt; '1'
), $atts));

$output = '';
$output .= '&lt;div class="blockquote-container"&gt;';
$output .= '&lt;div class="blockquote-inner style-'.$style.'"&gt;';
if($style == '3' || $style == '4')
$output .= '&lt;blockquote class="blockquote"&gt;&lt;i class="fa fa-quote-left"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;i class="fa fa-quote-right"&gt;&lt;/i&gt;&lt;/blockquote&gt;';
else
$output .= '&lt;blockquote class="blockquote"&gt;'.do_shortcode($content).'&lt;/blockquote&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_quote', 'shortcode_quote');

/***************** Button ****************/

function shortcode_button($atts, $content = null) {
extract(shortcode_atts(array(
'type' =&gt; 'medium',
'background_color' =&gt; '',
'link_url' =&gt; '#',
'icon' =&gt; '',
'icon_align' =&gt; 'left'
), $atts));

wp_reset_query();
$style_css = '';
if(!empty($background_color)):
$style_css .= 'background-color: #'.$background_color.';';
$icon_class = '';
else:
$icon_class = ' no-background';
endif;
$output = '';
$output .= '&lt;div class="button_content_inner"&gt;';
if(!empty($icon)){
if($icon_align == 'left')
$output .= '&lt;a href="'.$link_url.'" class="button animated button_'.$type.' '.$icon_align.'" style="'.$style_css.'"&gt;&lt;i class="fa '.$icon.'"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;/a&gt;';
if($icon_align == 'right')
$output .= '&lt;a href="'.$link_url.'" class="button animated button_'.$type.' '.$icon_align.'" style="'.$style_css.'"&gt;'.do_shortcode($content).'&lt;i class="fa '.$icon.'"&gt;&lt;/i&gt;&lt;/a&gt;';
}else{
$output .= '&lt;a href="'.$link_url.'" class="button animated button_'.$type.'" style="'.$style_css.'"&gt;'.do_shortcode($content).'&lt;/a&gt;';
}
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_button', 'shortcode_button');

/***************** Progress Bar  ****************/

function shortcode_progressbar_container($atts, $content = null, $code) {
extract(shortcode_atts(array(
'style' =&gt; '1',
), $atts));
$output = '';
$output .= '&lt;div class="progressbar-container"&gt;';
$output .= '&lt;div class="progressbar-content '.$style.'"&gt;';
$output .= do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('progressbar', 'shortcode_progressbar_container');

function shortcode_progressbar($atts, $content = null)
{
extract(shortcode_atts(array(
'value' =&gt; '90',
'color' =&gt;'FFFFFF',
'background_color' =&gt;'87CFC5',
'show_percentage' =&gt;'yes',
'style' =&gt; '1'
), $atts));
$output = '';
$output .= '&lt;div class="tm_progresbar style-'.$style.'"&gt;';

if($style == 4):
$output .=    '&lt;small class="progress_detail"&gt;';
$output .= do_shortcode($content);
if($show_percentage == 'yes') {
$output .= '&lt;span class="tm_progress_label"&gt;'.$value.'%&lt;/span&gt;';
}
$output .= '&lt;/small&gt;';
$output .= '&lt;div class="active_progresbar" style="color:#'.$color.'" data-value="'.$value.'" data-percentage-value="'.$value.'"&gt;';
else:
$output .= '&lt;div class="active_progresbar" style="color:#'.$color.'" data-value="'.$value.'" data-percentage-value="'.$value.'"&gt;';
$output .=    '&lt;small class="progress_detail" style="color:#'.$color.'"&gt;';
$output .= do_shortcode($content);
if($show_percentage == 'yes') {
$output .= '&lt;span class="tm_progress_label"&gt;'.$value.'%&lt;/span&gt;';
}
$output .= '&lt;/small&gt;';
endif;


$output .= '&lt;span class="value animated" data-animated="fadeInLeft" style="width:'.$value.'%; background-color:#'.$background_color.';"&gt;&lt;/span&gt;';
$output .=    '&lt;/div&gt;&lt;/div&gt;';

return $output;
}
add_shortcode('tm_progressbar', 'shortcode_progressbar');

/***************** PIE Chart ****************/
function shortcode_piechart($atts, $content = null)
{
extract(shortcode_atts(array(
'percentage' =&gt; 20,
'background_color' =&gt; '#87CFC5',
'title' =&gt; '',
), $atts));

$output = '';
$randomdValue = substr(str_shuffle("abcdefghijklmnopqrstuvwxyz123456789"), 0,2);
$output = '';

$output .='&lt;div class="tm_piechart column4"&gt;';
$output .='&lt;div class="chart_top"&gt;';
$output .='&lt;span class="chart_'.$randomdValue.' tmchat_wrapper animated" data-percent="'.$percentage.'"&gt;&lt;span class="percent" style="color:'.$background_color.';"&gt;&lt;/span&gt;&lt;/span&gt;';
$output .='&lt;/div&gt;';
$output .='&lt;div class="chart_bottom"&gt;';
if(!empty($title))
$output .='&lt;h2 class="chart_title"&gt;'.$title.'&lt;/h2&gt;';
$output .='&lt;div class="chart_desc"&gt;'.do_shortcode($content).'&lt;/div&gt;';
$output .='&lt;/div&gt;';
$output .='&lt;/div&gt;';

$output .= "&lt;script type='text/javascript'&gt;\n";
$output .= "\t jQuery(function() {\n";
$output .= "\t jQuery('.chart_".$randomdValue."').waypoint(function() {\n";
$output .= "\t jQuery(this).easyPieChart({\n";
$output .= "\t easing:'easeOutBounce',\n";
$output .= "\t animate: {duration: 2000, enabled: true},\n";
$output .= "\t barColor: '".$background_color."',\n";
$output .= "\t trackColor: '#EAEAEB',\n";
$output .= "\t scaleColor: '',\n";
$output .= "\t lineWidth: 8,\n";
$output .= "\t size: 130,\n";
$output .= "\t onStep: function(from, to, percent) { {\n";
$output .= "\t\t jQuery(this.el).find('.percent').text(Math.round(percent));\n";
$output .= "\t } \n";
$output .= "\t } }); \n";
$output .= "\t }, {
triggerOnce: true,
offset: 'bottom-in-view'
});\n";
$output .= "\t}); \n";
$output .= "&lt;/script&gt;\n\n";

return $output;
}
add_shortcode('tm_piechart', 'shortcode_piechart');

/***************** Social Icon  ****************/
function shortcode_socialicon($atts, $content = null)
{
extract(shortcode_atts(array(
'target' =&gt; '_blank',
'icon' =&gt; 'facebook',
'link' =&gt;'#',
), $atts));

$output = '';
$output .= '&lt;div class="tm_socialicon"&gt;';
$output .= '&lt;a href="'.$link.'" target="'.$target.'" title="'.$icon.'"&gt;&lt;i class="fa fa-'.$icon.'"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_socialicon', 'shortcode_socialicon');

/***************** Photo Shortcode ****************/
function shortcode_flickrphoto($atts, $content = null) {
extract(shortcode_atts(array(
'id' =&gt; '',
'count_no' =&gt; '',
), $atts));
$flickr_data = '&lt;script type="text/javascript" src="http://www.flickr.com/badge_code_v2.gne?count='.$count_no.'&amp;display=latest&amp;size=t&amp;layout=x&amp;source=user&amp;user='.$id.'"&gt;&lt;/script&gt; ';
return $flickr_data;
}
add_shortcode('tm_flickrphoto', 'shortcode_flickrphoto');// use:-[flickrbadge id="67176627@N04" count_no="6"]


/***************** Fancy Media ****************/
function shortcode_fancymedia($atts, $content = null) {
extract(shortcode_atts(array(
"media_type" =&gt; 'type1',
"enable_lightbox" =&gt; 'yes',
"align" =&gt; '',
"media_url" =&gt; '',
"media_img" =&gt; '',
"fancyimg_src" =&gt; '',
"image_alt" =&gt; '',
), $atts));

switch ($media_type) {
case 'type2' :
$media_type = 'noframe';
break;
default :
$media_type = 'frame';
break;
break;
}

if($fancyimg_src != NULL) {
$get_fancyimagepath = get_template_directory_uri() . '/images/' . $fancyimg_src;
} else {
$get_fancyimagepath = get_template_directory_uri() . '/images/megnor/no_image.jpg';
}

if($media_img != NULL) {
$get_mediaimagepath = get_template_directory_uri() . '/images/' . $media_img;
} else {
$get_mediaimagepath = get_template_directory_uri() . '/images/megnor/no_image.jpg';
}
$output = '';
$output .='&lt;div class="tm_fancymediacontent '.$media_type.' '.$align.'"&gt;&lt;div class="fancymedia_inner"&gt;';

if($media_url != NULL)
{
if($media_img != NULL)
{
$output .= '&lt;div class="media_top"&gt;';
$output .= '&lt;a href="'.$media_url.'" title="The Last Eggtion Hero"&gt;&lt;img src="'.$get_mediaimagepath.'" alt="'.$image_alt.'"/&gt;&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;div class="media_bottom"&gt;'.do_shortcode($content).'&lt;/div&gt;';
}
else
{
$output .= '&lt;div class="media_top"&gt;';
$output .= '&lt;iframe width="300" height="250" src="'.$media_url.'"&gt;&lt;/iframe&gt;';
$output .= '&lt;/div&gt;&lt;div class="media_bottom"&gt;'.do_shortcode($content).'&lt;/div&gt;';
}

}
else
{
$output .= '&lt;div class="media_top"&gt;';
if($enable_lightbox == "yes")
{
$output .= '&lt;a href="'.$get_fancyimagepath.'" class="mustang-gallery"&gt;&lt;img src="'.$get_fancyimagepath.'" alt="'.$image_alt.'"/&gt;&lt;/a&gt;';
}
else
{
$output .= '&lt;img src="'.$get_fancyimagepath.'" alt="'.$image_alt.'"/&gt;';
}
$output .= '&lt;/div&gt;&lt;div class="media_bottom"&gt;'.do_shortcode($content).'&lt;/div&gt;';
}
$output .= '&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_fancymedia', 'shortcode_fancymedia');

/***************** Logo ****************/

function shortcode_logo($atts, $content = null) {

extract(shortcode_atts(array(
'type' =&gt; 'grid',
'items_per_column' =&gt; 5,
'align' =&gt; 'left',
"border_color"=&gt; 'e6e4dc',
"border" =&gt; ''

), $atts));
$output = '';
if($border == 'yes')
{
$variables .= 'border-top:1px solid #'.$border_color.';';
}
$output .= '&lt;div id="brand-products" class="tm_logocontent '.$align.'"&gt;';
if($type == 'slider'):
$output .= '&lt;div id="'.$items_per_column.'_brand_carousel" class="brand-carousel tm-logo-content"&gt;';
else:
$output .= '&lt;div id="'.$items_per_column.'_brand_grid" class="brand-grid tm-logo-content"&gt;';
endif;
$output .=    do_shortcode($content).'&lt;/div&gt;&lt;/div&gt;';
return $output;
}

add_shortcode('tm_logo', 'shortcode_logo');

function shortcode_logoinner($atts, $content = null) {

extract(shortcode_atts(array(
"image" =&gt; '',
"link_url" =&gt; '',
"title" =&gt; 'Logo Image',
), $atts));

$output = '';
$output .= '&lt;div class="item brand_main"&gt;&lt;div class="product-block"&gt;&lt;a href="'.$link_url.'"&gt;&lt;img src="'.$image.'" alt="'.$title.'"/&gt;&lt;/a&gt;&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode("tm_logoinner", "shortcode_logoinner");

/***************** Banner ****************/

function shortcode_banner($atts, $content = null)
{
extract(shortcode_atts(array(
'backgroung_img' =&gt; '',
'link_url' =&gt; '#',
'title' =&gt; '',
'description' =&gt; '',
'textalign' =&gt; '',
'classname' =&gt; ''
), $atts));

if($backgroung_img != NULL) {
$get_imagepath = $backgroung_img;
} else {
$get_imagepath = get_template_directory_uri() . '/images/megnor/no_image.jpg';
}
$variables='text-align:'.$textalign.';';
$output = '';
$output .='&lt;div class="tm_banner column1 '.$classname.'" style="'.$variables.'"&gt;';
$output .='&lt;div class="tm_banner_inner"&gt;';
$output .='&lt;a href="'.$link_url.'" target="_Blank"&gt;';
$output .='&lt;img src="'.$get_imagepath.'" alt="" /&gt;';
$output .='&lt;/a&gt;';
$output .='&lt;/div&gt;';
if(!empty($title))
$output .='&lt;div class="title"&gt;'.$title.'&lt;/div&gt;';
if(!empty($description))
$output .='&lt;div class="description"&gt;'.$description.'&lt;/div&gt;';
$output .='&lt;/div&gt;';
return $output;
}
add_shortcode('tm_banner', 'shortcode_banner');

/***************** Home Sub Banner ****************/

function shortcode_sub_banner($atts, $content = null)
{
extract(shortcode_atts(array(
'classname' =&gt; ''
), $atts));
$output = '';
$output .='&lt;div class="tm_sub_banner '.$classname.'"&gt;';
$output .= do_shortcode($content);
$output .='&lt;/div&gt;';
return $output;
}
add_shortcode('tm_sub_banner', 'shortcode_sub_banner');

/***************** Banner slider ****************/

function shortcode_single_slide($atts, $content = null, $code) {
extract(shortcode_atts(array(
'title' =&gt; '',
), $atts));

$output = '';
$output .= '&lt;div class="banner-slider-container"&gt;';
$output .= '&lt;div class="slider-container-inner"&gt;';
$output .= '&lt;div class="title"&gt;'.$title.'&lt;/div&gt;';
$output .= '&lt;div class="flexslider"&gt;';
$output .= '&lt;ul class="slides"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/ul&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('slider', 'shortcode_single_slide');

function shortcode_single_slider($atts, $content = null)
{
extract(shortcode_atts(array(
'image' =&gt; '',
'link' =&gt; '',
'height' =&gt; '',
'width' =&gt; '',
), $atts));
$output = '';
$output .= '&lt;li&gt;&lt;div class="banner-image"&gt;';
if(!empty($link)):
$output .= '&lt;a target="_Blank" href="'.$link.'"&gt;&lt;img src="'.$image.'" alt="" height="'.$height.'" width="'.$width.'" class="vv" /&gt;&lt;/a&gt;';
else:
$output .= '&lt;img src="'.$image.'" alt="" class="vv" /&gt;';
endif;
$output .= '&lt;/li&gt;&lt;/div"&gt;';
return $output;
}
add_shortcode('slide', 'shortcode_single_slider');

/***************** Gallery  ****************/

function shortcode_gallery($attr) {
$post = get_post();
static $instance = 0;
$instance++;

if ( ! empty( $attr['ids'] ) ) {
// 'ids' is explicitly ordered, unless you specify otherwise.
if ( empty( $attr['orderby'] ) )
$attr['orderby'] = 'post__in';
$attr['include'] = $attr['ids'];
}

#Allow plugins/themes to override the default gallery template.
$output = apply_filters('post_gallery', '', $attr);

if ( $output != '' )
return $output;

# We're trusting author input, so let's at least make sure it looks like a valid orderby statement
if ( isset( $attr['orderby'] ) ) {
$attr['orderby'] = sanitize_sql_orderby( $attr['orderby'] );
if ( !$attr['orderby'] )
unset( $attr['orderby'] );
}

extract(shortcode_atts(array(
'type'      =&gt; 'grid',
'order'      =&gt; 'ASC',
'orderby'    =&gt; 'menu_order ID',
'id'         =&gt; $post-&gt;ID,
'itemtag'    =&gt; 'dl',
'icontag'    =&gt; 'dt',
'captiontag' =&gt; 'dd',
'columns'    =&gt; 3,
'size'       =&gt; 'thumbnail',
'include'    =&gt; '',
'exclude'    =&gt; ''
), $attr));

$id = intval($id);
if ( 'RAND' == $order )
$orderby = 'none';

if ( !empty($include) )
{
$_attachments = get_posts( array('include' =&gt; $include, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );

$attachments = array();
foreach ( $_attachments as $key =&gt; $val ) {
$attachments[$val-&gt;ID] = $_attachments[$key];
}
}
elseif ( !empty($exclude) )
{
$attachments = get_children( array('post_parent' =&gt; $id, 'exclude' =&gt; $exclude, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
}
else
{
$attachments = get_children( array('post_parent' =&gt; $id, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
}

if ( empty($attachments) )
return '';

if ( is_feed() ) {
$output = "\n";
foreach ( $attachments as $att_id =&gt; $attachment )
$output .= wp_get_attachment_link($att_id, $size, true) . "\n";
return $output;
}

$itemtag = tag_escape($itemtag);
$captiontag = tag_escape($captiontag);
$icontag = tag_escape($icontag);
$valid_tags = wp_kses_allowed_html( 'post' );

if ( ! isset( $valid_tags[ $itemtag ] ) )
$itemtag = 'dl';
if ( ! isset( $valid_tags[ $captiontag ] ) )
$captiontag = 'dd';
if ( ! isset( $valid_tags[ $icontag ] ) )
$icontag = 'dt';

$columns = intval($columns);


$selector = "gallery-{$instance}";


$size_class = sanitize_html_class( $size );

$gallery_div = "&lt;div id='$selector' class='gallery galleryid-{$id} gallery-columns-{$columns} gallery-size-{$size_class}'&gt;";
$output = apply_filters( 'gallery_style', $gallery_style . "\n\t\t" . $gallery_div );

$i = 0;
foreach ( $attachments as $id =&gt; $attachment )
{



$link = isset($attr['link']) &amp;&amp; 'file' == $attr['link'] ? wp_get_attachment_link($id, $size, false, false) : wp_get_attachment_link($id, $size, true, false);

$output = '';
$output .= "&lt;{$itemtag} class='gallery-item'&gt;";
$output .= "
&lt;{$icontag} class='gallery-icon'&gt;
$link
&lt;/{$icontag}&gt;";
if ( $captiontag &amp;&amp; trim($attachment-&gt;post_excerpt) ) {
$output .= "
&lt;{$captiontag} class='wp-caption-text gallery-caption'&gt;
" . wptexturize($attachment-&gt;post_excerpt) . "
&lt;/{$captiontag}&gt;";
}
$output .= "&lt;/{$itemtag}&gt;";
if ( $columns &gt; 0 &amp;&amp; ++$i % $columns == 0 )
$output .= '&lt;br style="clear: both" /&gt;';
}

$output .= "
&lt;br style='clear: both;' /&gt;
&lt;/div&gt;\n";

return $output;
}

add_shortcode('tm_gallery', 'shortcode_gallery');


/*============ testing ===========*/
function ContactButton($params, $content = null) {

extract(shortcode_atts(array(
'url' =&gt; '/contact-us',
'type' =&gt; 'style1'
), $params));

return
'&lt;a href="' . $url . '" class="button ' . $type. '"&gt;' . ucwords($content) . '&lt;/a&gt;';

}
add_shortcode('button','ContactButton');

// callout box
function CalloutBox($params, $content = null) {

extract(shortcode_atts(array(
'type' =&gt; 'style1'
), $params));

return
'&lt;div class="callout ' . $type . '"&gt;' . $content . '&lt;/div&gt;';

}
add_shortcode('callout','CalloutBox');

/***************** Portfolio Filter ****************/

function shortcode_portfolio_filter_container($atts, $content = null, $code) {
global $logotype;
extract(shortcode_atts(array(
'items_per_column' =&gt; 4
), $atts));

if($items_per_column == '1'):
$width = 550;
$height = 550;
$desc_limit = 550;
elseif($items_per_column == '2'):
$width = 600;
$height = 600;
$desc_limit = 450;
elseif($items_per_column == '3'):
$width = 600;
$height = 600;
$desc_limit = 250;
else:
$width = 600;
$height = 600;
$desc_limit = 80;
endif;
$categories = get_categories('hide_empty=0&amp;orderby=name&amp;taxonomy=portfolio_categories');
$output = '';
$output .= '&lt;div class="clearfix portfolio-filter-container filter-container"&gt;';
$output .= '&lt;section id="portfolio_filter_options" class="options category-container""&gt;';
$output .= '&lt;ul id="filters" class="option-set"  data-option-key="filter"&gt;';
$output .= '&lt;li&gt;&lt;a href="#show-all" data-option-value="*" class="selected"&gt;Show All&lt;/a&gt;&lt;/li&gt;';
foreach ($categories as $category_item ) {
$output .= '&lt;li&gt;&lt;a href="#'.$category_item-&gt;slug.'" data-option-value=".'.$category_item-&gt;slug.'"&gt;'.$category_item-&gt;cat_name.'&lt;/a&gt;&lt;/li&gt;';
}
$output .= '&lt;/ul&gt;&lt;/section&gt;';
$output .= '&lt;div id="portfolio_filter" class="portfolio-container portfolios portfolio-filter clearfix da-thumbs portfolio-cols-'.$items_per_column.'"&gt;';
foreach ($categories as $category_item ):
$paged = ( isset( $my_query_array['paged'] ) &amp;&amp; !empty( $my_query_array['paged'] ) ) ? $my_query_array['paged'] : 1;
$args = array(
'post_type' =&gt; 'portfolio',
'post_status' =&gt; 'publish',
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'portfolio_categories',
'field' =&gt; 'id',
'terms' =&gt; $category_item-&gt;term_id,
'paged' =&gt; $paged
)
)
);
query_posts($args);
while (have_posts()) : the_post();
$image = templatemela_get_first_post_images(get_the_ID());
$src = mr_image_resize($image, $width, $height, true, 't', false);
if( empty ( $src ) || $src == 'image_not_specified' ):
$src = get_template_directory_uri()."/images/megnor/placeholder.png";
$src = mr_image_resize($src, $width, $height, true, $align, false);
endif;
$output .= '&lt;div class="'.$category_item-&gt;slug.' main item single-portfolio"&gt;';
$output .= '&lt;div class="image image-block"&gt;';
$output .= '&lt;img src="'.$src.'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
$output .= '&lt;div class="block_hover"&gt;';
$output .= '&lt;h1 class="entry-title"&gt;'.get_the_title().'&lt;/h1&gt;';
$output .= '&lt;div class="links"&gt;';
$output .= '&lt;a href="'.$image.'" class="icon mustang-gallery"&gt;&lt;i class="fa fa-search"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;a href="'.get_permalink().'" class="icon"&gt;&lt;i class="fa fa-link"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
endwhile;
endforeach;
wp_reset_query();
$output .= '&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_portfolio_filter', 'shortcode_portfolio_filter_container');

/***************** Portfolio Slider ****************/

function shortcode_portfolio_slider_container($atts, $content = null, $code) {
global $logotype;
extract(shortcode_atts(array(
'category' =&gt; '',
'type' =&gt; 'slider',
'items_per_column' =&gt; 3,
'number_of_posts' =&gt; 10,
'layout' =&gt; 'dark'
), $atts));

if(!empty($category)):
$term_id = $category;
$args = array(
'post_type' =&gt; 'portfolio',
'post_status' =&gt; 'publish',
'posts_per_page' =&gt; $number_of_posts,
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'portfolio_categories',
'field' =&gt; 'id',
'terms' =&gt; $term_id
)
)
);
else:
$args = array(
'post_type' =&gt; 'portfolio',
'post_status' =&gt; 'publish',
'posts_per_page' =&gt; "'".$number_of_posts."'"
);
endif;
$array_posts = query_posts($args);
$count = count($array_posts);
$output = '';
if($count &gt; 0):
$output .= '&lt;div class="portfolio-container"&gt;';
if($type == 'slider'):
if($count &gt; $items_per_column)
$output .= '&lt;div id="'.$items_per_column.'_portfolio_carousel" class="portfolio-carousel"&gt;';
else
$output .= '&lt;div id="'.$items_per_column.'_portfolio_grid" class="portfolio-grid"&gt;';
else:
$output .= '&lt;div id="'.$items_per_column.'_portfolio_grid" class="portfolio-grid"&gt;';
endif;
$i = 1;
while (have_posts()) : the_post();
if($i % $items_per_column == 1 )
$class = "first";
elseif($i % $items_per_column == 0 )
$class = "last";
else
$class = "";
if($items_per_column == '1'):
$width = 550;
$height = 550;
elseif($items_per_column == '2'):
$width = 450;
$height = 450;
elseif($items_per_column == '3'):
$width = 300;
$height = 300;
else:
$width = 250;
$height = 250;
endif;
$image = templatemela_get_first_post_images(get_the_ID());
$image_src = mr_image_resize($image, $width, $height, true, 't', false);
if(empty($image_src))
$image_src = get_template_directory_uri()."/images/megnor/placeholder.png";
$output .= '&lt;div class="item portfolio-main"&gt;';
$output .= '&lt;div class="product-block single-portfolio '.$class.' '.$layout.'"&gt;';
$output .= '&lt;div class="portfolio-image"&gt;';
$output .= '&lt;div class="portfolio-image_inner"&gt;';
$output .= '&lt;img src="'.$image_src.'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
$output .= '&lt;div class="other-box"&gt;';
$output .= '&lt;div class="links"&gt;';
$output .= '&lt;a href="'.$image.'" title="Click to view Full Image" class="icon mustang-gallery"&gt;&lt;i class="fa fa-search"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;a href="'.get_permalink().'" title="Click to view Read More" class="icon"&gt;&lt;i class="fa fa-link"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="portfolio-title"&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/div&gt;&lt;/a&gt;';
$output .= '&lt;div class="portfolio-description"&gt;'.templatemela_portfolio_excerpt(100).'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$i++;
endwhile;
$output .= '&lt;/div&gt;';
wp_reset_query();
$output .= '&lt;/div&gt;';
else:
$output .= '&lt;div class="no-result"&gt;No results found...&lt;/div&gt;';
endif;
return $output;
}
add_shortcode('tm_portfolio_slider', 'shortcode_portfolio_slider_container');

/*============ Portfolio ===========*/

function shortcode_portfolio($atts, $content = null, $code) {
extract(shortcode_atts(array(
'column' =&gt; 4,
'cat' =&gt; '',
'max' =&gt; '12'
), $atts));

$output = '';
$paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
$terms = array();
if ($cat != '') {
$cat = preg_replace('/\s*,\s*/', ',', $cat);
foreach(explode(',', $cat) as $term_name) {
$terms[] = get_term_by('name', $term_name, 'portfolio_categories');
}
foreach($terms as $term) {
$term_ids[] = $term-&gt;term_id;
}
$args = array(
'posts_per_page' =&gt; $max,
'paged' =&gt; $paged,
'post_type' =&gt; 'portfolio',
'post_status' =&gt; 'publish',
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'portfolio_categories',
'field' =&gt; 'id',
'terms' =&gt; $term_ids
)
)
);
} else {
$args = array(
'posts_per_page' =&gt; $max,
'paged' =&gt; $paged,
'post_type' =&gt; 'portfolio',
'post_status' =&gt; 'publish'
);
}
query_posts($args);
if($column == 1){
$width = 1200;
$excerpt_length = 180;
$column = 1;
}else if($column == 2){
$width = 600;
$excerpt_length = 180;
$column = 2;
}else if($column == 3){
$width = 400;
$excerpt_length = 120;
$column = 3;
}else if($column == 4){
$width = 300;
$excerpt_length =80;
$column = 4;
}else {
$width = 300;
$column = 4;
}

$output = '&lt;div class="portfolios"&gt;';
$output .= '&lt;ul class="portfolio_'.$column.'column da-thumbs"&gt;';
$num_layout =  substr($column, 0, 1);
$i = 1;
while(have_posts()) {
the_post();
$terms = get_the_terms(get_the_ID(), 'portfolio_categories');
if ( strlen( $img = get_the_post_thumbnail( get_the_ID()) ) ):
$image = wp_get_attachment_url( get_post_thumbnail_id(get_the_ID()) );
else:
$image = templatemela_get_first_post_images(get_the_ID());
endif;
$src = mr_image_resize($image, $width, $width, true, 'left', false);
if( empty ( $src ) || $src == 'image_not_specified' ):
$src = get_template_directory_uri()."/images/megnor/placeholder.png";
$image = $src;
$src = mr_image_resize($src, $width, $width, true, 'left', false);
endif;
?&gt;
&lt;?php $terms_slug = array();
if (is_array($terms)) {
foreach($terms as $term) {
$terms_slug[] = $term-&gt;slug;
}
}
if($i % $num_layout == 0)
$li_class = "last";
else if($i % $num_layout == 1)
$li_class = "first";
else
$li_class = "inner";
$output .= '&lt;li class="'.$li_class.'"&gt;';
$more = get_post_meta(get_the_ID(), '_more', true);
$output .= '&lt;div class="main"&gt;&lt;div class="image-block"&gt;';
if(get_option('portfolio','display_image') || $column == 1):
$output .= '&lt;a href= "'.$image.'" class="mustang-gallery"&gt;';
$output .= '&lt;img class="image1" src="'.$src.'"/ &gt;';
$output .= '&lt;/a&gt;';
endif;
$output .= '&lt;div class="other-box"&gt;';
$output .= '&lt;div class="links"&gt;';
$output .= '&lt;a href="'.$image.'" title="Click to view Full Image" class="icon mustang-gallery"&gt;&lt;i class="fa fa-search"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;a href="'.get_permalink().'" title="Click to view Read More" class="icon"&gt;&lt;i class="fa fa-link"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;h5&gt;&lt;a href="'.get_permalink().'"&gt;'.get_the_title().'&lt;/a&gt;&lt;/h5&gt;';
$output .=  templatemela_portfolio_excerpt($excerpt_length);
$output .= '&lt;/li&gt;';
$i++;
}
$output .= '&lt;/ul&gt;';
$output .= templatemela_shortcode_paging_nav();
$output .= '&lt;/div&gt;';
wp_reset_query();
return $output;
}

add_shortcode('tm_portfolio', 'shortcode_portfolio');

/*============ Faqs ===========*/
function shortcode_faqs($atts, $content = null, $code) {
extract(shortcode_atts(array(
'style' =&gt; '1',
'category' =&gt; ''
), $atts));
$output = '';
$output .= '&lt;div class="faqs-container"&gt;';
$output .= '&lt;div class="faqs-content style-'.$style.'"&gt;';

if(!empty($category)):
$term_id = $category;
$args = array(
'post_type' =&gt; 'faq',
'post_status' =&gt; 'publish',
'posts_per_page' =&gt; '50',
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'faq_categories',
'field' =&gt; 'id',
'terms' =&gt; $term_id
)
)
);
query_posts($args);
$term = get_term( $term_id, 'faq_categories' );
$output .= '&lt;h1 class="small-title"&gt;'.$term-&gt;name.'&lt;/h1&gt;';
$output .= '&lt;div class="faqs-category-container"&gt;';
while (have_posts()) : the_post();
if($style == '1'):
$output .= '&lt;div class="single-faq toogle_div"&gt;';
$output .= '&lt;a class="tog" href="#"&gt;&lt;span class="faq_title"&gt;'. get_the_title() .' &lt;/span&gt;&lt;/a&gt;';
$output .= '&lt;div class="tab_content"&gt;'.get_the_content().'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
endif;
if($style == '2'):
$output .= '&lt;div class="single-faq"&gt;';
$output .= '&lt;div class="title"&gt;'.get_the_title().'&lt;/div&gt;';
$output .= '&lt;div class="content"&gt;'.get_the_content().'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
endif;
endwhile;
$output .= '&lt;/div&gt;';
else:
$categories = get_categories('hide_empty=0&amp;orderby=name&amp;taxonomy=faq_categories');
foreach ($categories as $category_item ) {
$args = array(
'post_type' =&gt; 'faq',
'post_status' =&gt; 'publish',
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'faq_categories',
'field' =&gt; 'id',
'terms' =&gt; $category_item-&gt;term_id
)
)
);
query_posts($args);
$output .= '&lt;h1 class="small-title"&gt;'.$category_item-&gt;name.'&lt;/h1&gt;';
$output .= '&lt;div class="faqs-category-container"&gt;';
while (have_posts()) : the_post();
if($style == '1'):
$output .= '&lt;div class="single-faq toogle_div"&gt;';
$output .= '&lt;div class="title"&gt;&lt;a class="tog" href="#"&gt; &lt;span class="cp_plus"&gt; &lt;span class="vert_line"&gt;&lt;/span&gt; &lt;span class="horiz_line"&gt;&lt;/span&gt; &lt;/span&gt; &lt;span class="faq_title"&gt;'. get_the_title() .' &lt;/span&gt;&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;div class="tab_content"&gt;'.get_the_content().'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
endif;
if($style == '2'):
$output .= '&lt;div class="single-faq"&gt;';
$output .= '&lt;div class="title"&gt;'.get_the_title().'&lt;/div&gt;';
$output .= '&lt;div class="content"&gt;'.get_the_content().'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
endif;
endwhile;
$output .= '&lt;/div&gt;';
}
endif;
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
wp_reset_query();
return $output;
}
add_shortcode('faqs', 'shortcode_faqs');

function shortcode_single_static_link($atts, $content = null) {

extract(shortcode_atts(array(
"link" =&gt; '',
"title" =&gt; '',
), $atts));

$output = '';
$output .= '&lt;div class="single-link"&gt;&lt;a href="'.$link.'"&gt;'.$title.'&lt;/a&gt;&lt;/div&gt;';
return $output;
}
add_shortcode("single_link", "shortcode_single_static_link");

/********************Title***************/
function shortcode_title($atts, $content = null) {

extract(shortcode_atts(array(
'size' =&gt; 'big',
'type' =&gt; 'simple',
'color' =&gt; '',
'align' =&gt; '',
'classname' =&gt; ''
), $atts));

$output = '';
$output .= '&lt;div class="shortcode-title '.$align.' '.$classname.'"&gt;';

if(!empty($color))
$output .= '&lt;h1 class="'.$type.'-type '.$size.'-title" style="color:#'.$color.';"&gt;'.do_shortcode($content).'&lt;/h1&gt;';
else
$output .= '&lt;h1 class="'.$type.'-type '.$size.'-title"&gt;'.do_shortcode($content).'&lt;/h1&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode("title", "shortcode_title");

function shortcode_our_features($atts, $content = null) {
extract(shortcode_atts(array(
"icon" =&gt; '',
"title" =&gt; '',
"read_more_text" =&gt; 'Read More',
"read_more_link" =&gt; '',
), $atts));

$output = '';
$output .= '&lt;div class="feature-container"&gt;';
$output .= '&lt;div class="feature-content"&gt;';
if(!empty($icon))
$output .= '&lt;div class="icon"&gt;&lt;i class="'.$icon.'"&gt;&lt;/i&gt;&lt;/div&gt;';
if(!empty($title))
$output .= '&lt;div class="title"&gt;'.$title.'&lt;/div&gt;';
$output .= '&lt;div class="description"&gt;'.do_shortcode($content).'&lt;/div&gt;';
if(!empty($read_more_link))
$output .= '&lt;a herf="'.$read_more_link.'" class="other-read-more"&gt;'.$read_more_text.'&lt;/a&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode("feature", "shortcode_our_features");

/***************** Features ****************/

function shortcode_about($atts, $content = null)
{
extract(shortcode_atts(array(
'title' =&gt; '',
'link_text' =&gt; 'Read More',
'link_url' =&gt; '#',
'image' =&gt; '',
'image_align' =&gt; 'right',
'title_margin' =&gt; '20px 0 30px'
), $atts));

$output = '';
$output .='&lt;div class="tm_about"&gt;';
$output .='&lt;div class="tm_about_inner image-'.$image_align.'"&gt;';
if(!empty($image)):
$output .='&lt;div class="about_image one_half"&gt;';
$output .='&lt;img src="'.$image.'" alt="" /&gt;';
$output .='&lt;/div&gt;';
endif;
if(!empty($image))
$output .='&lt;div class="about_content one_half"&gt;';
else
$output .='&lt;div class="about_content"&gt;';
$output .='&lt;h3 class="title" style="margin:'.$title_margin.'"&gt;'.$title.'&lt;/h3&gt;';
$output .='&lt;div class="description"&gt;'.do_shortcode($content).'&lt;/div&gt;';
$output .='&lt;div class="readmore"&gt;&lt;a href="'.$link_url.'" title="'.$link_text.'"&gt;'.$link_text.'&lt;i class="fa fa-arrow-right"&gt;&lt;/i&gt;&lt;/a&gt;&lt;/div&gt;';
$output .='&lt;/div&gt;';
$output .='&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_about', 'shortcode_about');

/***************** Overlap images ****************/

function shortcode_overlap_images($atts, $content = null)
{
extract(shortcode_atts(array(
), $atts));

$output = '';
$output .='&lt;div class="tm_overlap_images"&gt;';
$output .='&lt;div class="tm_overlap_images_inner"&gt;';
$output .='&lt;ul class="images"&gt;';
$output .= do_shortcode($content);
$output .='&lt;/ul&gt;';
$output .='&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('tm_overlap_images', 'shortcode_overlap_images');

function shortcode_overlap_image($atts, $content = null)
{
extract(shortcode_atts(array(
'image' =&gt; '',
'link_url' =&gt; '',
'margin' =&gt; '0',
'textalign' =&gt; ''
), $atts));
$output = '';
$variables = '';


$variables .= 'margin:'.$margin.';';
$variables .= 'text-align:'.$textalign.';';
$output .='&lt;li class="banner" style="'.$variables.';"&gt;&lt;a href="'.$link_url.'" target="_blank"&gt;&lt;img class="animated" data-animated="fadeInLeft" src="'.$image.'" alt=""/&gt;&lt;span class="hover_glass"&gt; &lt;/span&gt; &lt;/a&gt;&lt;/li&gt;';
return $output;
}
add_shortcode("tm_single_image", "shortcode_overlap_image");

/***************** Services ****************/

function shortcode_home_services($atts, $content = null) {
extract(shortcode_atts(array(
"color" =&gt; '464E55',
"icon_background_color" =&gt; '',
"icon" =&gt; 'fa-arrows-alt',
"title" =&gt; '',
"link_text" =&gt; '',
"link_url" =&gt; '',
"style" =&gt; '1'
), $atts));

$style_css = 'color:#'.$color.';';
if(!empty($icon_background_color)):
$style_css .= 'background-color: #'.$icon_background_color.';';
$icon_class = '';
else:
$icon_class = ' no-background';
endif;

$output = '';
$output .= '&lt;div class="service hb-animate-element bottom-to-top style-'.$style.'"&gt;';
$output .= '&lt;div class="service-content style-'.$style.'"&gt;';

if($style == '1' || $style == '2'):
if(!empty($icon))
$output .= '&lt;div class="icon"&gt;&lt;i class="service-icon fa '.$icon.$icon_class.'" style="'.$style_css.'"&gt;&lt;/i&gt;&lt;/div&gt;';
$output .= '&lt;div class="service-content"&gt;';
if(!empty($title))
$output .= '&lt;div class="title service-text"&gt;'.$title.'&lt;/div&gt;';
endif;

if($style == '3'):
$output .= '&lt;div class="service-top"&gt;';
if(!empty($icon))
$output .= '&lt;div class="icon"&gt;&lt;i class="service-icon fa '.$icon.$icon_class.'" style="'.$style_css.'"&gt;&lt;/i&gt;&lt;/div&gt;';
if(!empty($title))
$output .= '&lt;div class="title service-text"&gt;'.$title.'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="service-content"&gt;';
endif;

if($style == '4'):
if(!empty($title))
$output .= '&lt;div class="title service-text"&gt;'.$title.'&lt;/div&gt;';
if(!empty($icon))
$output .= '&lt;div class="icon"&gt;&lt;i class="service-icon fa '.$icon.$icon_class.'" style="color:#'.$color.';background-color: #'.$icon_background_color.';"&gt;&lt;/i&gt;&lt;/div&gt;';
$output .= '&lt;div class="service-content"&gt;';
endif;

$output .= '&lt;div class="description other-font"&gt;'.do_shortcode($content).'&lt;/div&gt;';

if(!empty($link_text)):
if(!empty($link_url)):
$output .= '&lt;div class="service-read-more other-font"&gt;&lt;a herf="'.$link_url.'" class="other-read-more"&gt;'.$link_text.'&lt;i class="fa fa-arrow-right"&gt;&lt;/i&gt;&lt;/a&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="service-read-more other-font"&gt;'.$link_text.'&gt;&lt;/div&gt;';
endif;
endif;

$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode("service", "shortcode_home_services");


/***************** Code ****************/

function shortcode_code($atts, $content = null) {

extract(shortcode_atts(array(
'style'    =&gt; '1'
), $atts));

$output = '';
$output .= '&lt;div class="code"&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_code', 'shortcode_code');
/*============ Container ===========*/
function shortcode_container($atts, $content = null){
extract(shortcode_atts(array(
'background_color' =&gt; '',
'background_image' =&gt; '',
'background_repeat' =&gt; 'no-repeat',
'background_attachment' =&gt; 'fixed',
'parallex' =&gt; true,
'background_size' =&gt; 'cover',
'padding' =&gt; '0',
'margin' =&gt; '0',
'align'=&gt; '',
'color'=&gt; '',
'border_color'=&gt; '',
'classname'=&gt;'',
'overflow'=&gt;'hidden'
), $atts));

$variables  = '';
if(!empty($background_color))
$variables .= 'background-color: #'.$background_color.';';
$variables .= 'padding:'.$padding.';';
$variables .= 'margin:'.$margin.';';
$variables .= 'border-top:1px solid #'.$border_color.';';
if(!empty($color))
$variables .= 'color:#'.$color.';';
$variables .= 'overflow:'.$overflow.';';
if(!empty($background_image)):
$variables .= 'background-image: url('.$background_image.');';
$variables .= 'background-repeat:'.$background_repeat.';';
$variables .= 'background-size:'.$background_size.';';
$variables .= 'background-attachment:'.$background_attachment.';';
endif;
$output = '';
$output .= '&lt;div class="main-container '.$align.' '.$classname.'" style="'.$variables.');"&gt;';
$output .= '&lt;div class="inner-container"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('container', 'shortcode_container');

/*============ One half ===========*/
function shortcode_one_half($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="one_half"&gt;';
$output .= '&lt;div class="one_half_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('one_half', 'shortcode_one_half');

/*============ Inner One half ===========*/
function shortcode_inner_one_half($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="one_half"&gt;';
$output .= '&lt;div class="one_half_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('inner_one_half', 'shortcode_inner_one_half');

/*============ One third ===========*/
function shortcode_one_third($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left',
'padding' =&gt; '',
'classname'=&gt; ''
), $atts));

$output = '';
$output .= '&lt;div class="one_third '.$classname.'"&gt;';
$output .= '&lt;div class="one_third_inner content_inner '.$align.'" style="margin:'.$margin.';padding:'.$padding.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('one_third', 'shortcode_one_third');

/*============ One fourth ===========*/
function shortcode_one_fourth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="one_fourth"&gt;';
$output .= '&lt;div class="one_fourth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('one_fourth', 'shortcode_one_fourth');

/*============ One Fifth ===========*/
function shortcode_one_fifth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="one_fifth"&gt;';
$output .= '&lt;div class="one_fifth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('one_fifth', 'shortcode_one_fifth');

/*============ One sixth ===========*/
function shortcode_one_sixth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="one_sixth"&gt;';
$output .= '&lt;div class="one_sixth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('one_sixth', 'shortcode_one_sixth');

/*============ Two third ===========*/
function shortcode_two_third($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="two_third"&gt;';
$output .= '&lt;div class="two_third_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('two_third', 'shortcode_two_third');

/*============ Two Fifth ===========*/
function shortcode_two_fifth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="two_fifth"&gt;';
$output .= '&lt;div class="two_fifth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('two_fifth', 'shortcode_two_fifth');

/*============ Three Fourth ===========*/
function shortcode_three_fourth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="three_fourth"&gt;';
$output .= '&lt;div class="three_fourth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('three_fourth', 'shortcode_three_fourth');

/*============ Three Fifth ===========*/
function shortcode_three_fifth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="three_fifth"&gt;';
$output .= '&lt;div class="three_fifth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('three_fifth', 'shortcode_three_fifth');

/*============ Four Fifth ===========*/
function shortcode_four_fifth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="four_fifth"&gt;';
$output .= '&lt;div class="four_fifth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('four_fifth', 'shortcode_four_fifth');

/*============ Four Fifth ===========*/
function shortcode_five_sixth($atts, $content = null){
extract(shortcode_atts(array(
'content_width' =&gt; '100%',
'margin' =&gt; '0',
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="five_sixth"&gt;';
$output .= '&lt;div class="five_sixth_inner content_inner '.$align.'" style="margin:'.$margin.';width:'.$content_width.';"&gt;';
$output .=    do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('five_sixth', 'shortcode_five_sixth');

/***************** Static Text ****************/

function shortcode_static_text($atts, $content = null){
extract(shortcode_atts(array(
'align' =&gt; 'left'
), $atts));

$output = '';
$output .= '&lt;div class="static-text-container '.$align.'"&gt;';
$output .= '&lt;div class="text"&gt;'.do_shortcode($content).'&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}

add_shortcode('text', 'shortcode_static_text');


/***************** Blog Posts ****************/
function shortcode_blog_posts_container($atts, $content = null, $code) {
extract(shortcode_atts(array(
'type' =&gt; 'grid',
'items_per_column' =&gt; 3,
'number_of_posts' =&gt; 10,
'category' =&gt; ''
), $atts));

$i = 1;
$post ="";
wp_reset_postdata();
$args = array(
'post_type' =&gt; 'post',
'tax_query' =&gt; array(
array(
'taxonomy' =&gt; 'post_format',
'field' =&gt; 'slug',
'terms' =&gt; array( 'post-format-link', 'post-format-image', 'post-format-quote', 'post-format-gallery','post-format-audio','post-format-video','post-format-status','post-format-chat','post-format-aside' ),
'operator' =&gt; 'NOT IN'
)
),
'posts_per_page' =&gt; $number_of_posts,
'post_status' =&gt; 'publish',
'category_name' =&gt; $category,
'orderby' =&gt; 'date'
);
$output = '';
$blog_array = new WP_Query( $args );
$count = $blog_array-&gt;post_count;
$output = '';
if ( $blog_array-&gt;have_posts() ):
$output .= '&lt;div id="blog-posts-products" class="blog-posts-content posts-content main-ul"&gt;';
if($type == "slider") {
if($count &gt; $items_per_column)
$output .= '&lt;div id="'.$items_per_column.'_blog_carousel" class="slider blog-carousel"&gt;';
else
$output .= '&lt;div id="blog_grid" class="blog-grid grid cols-'.$items_per_column.'"&gt;';
} else {
$output .= '&lt;div id="blog_grid" class="blog-grid grid cols-'.$items_per_column.'"&gt;';
}

while ( $blog_array-&gt;have_posts() ) : $blog_array-&gt;the_post();

if($i % $items_per_column == 1 )
$class = " first";
elseif($i % $items_per_column == 0 )
$class = " last";
else
$class = "";
$post_day = get_the_date('j');
$post_month = get_the_date('M');
$post_year = get_the_date('Y');
$post_author = get_the_author();
$args = array(
'status' =&gt; 'approved',
'number' =&gt; '5',
'post_id' =&gt; get_the_ID()
);
$comments = wp_count_comments(get_the_ID());
if ( has_post_thumbnail() &amp;&amp; ! post_password_required() ) :
$post_thumbnail_id = get_post_thumbnail_id();
$image = wp_get_attachment_url( $post_thumbnail_id );
else:
$image = get_template_directory_uri()."/images/placeholders/placeholder.jpg";
endif;
$src = mr_image_resize($image, 370, 200, true, 'c', false);
if( empty ( $src ) || $src == 'image_not_specified' ):
$src = get_template_directory_uri()."/images/megnor/placeholder.png";
$src = mr_image_resize($src, 370, 200, true, 't', false);
endif;
$output .= '&lt;div class="item container '.$class.'"&gt;';
$output .= '&lt;div class="container-inner"&gt;';
$output .= '&lt;div class="post-image"&gt;';
$output .= '&lt;img src="'.$src.'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
$output .= '&lt;div class="block_hover"&gt;';
$output .= '&lt;div class="links"&gt;';
$output .= '&lt;a href="'.$image.'" class="icon mustang-gallery"&gt;&lt;i class="fa fa-search"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;a href="'.get_permalink().'" class="icon"&gt;&lt;i class="fa fa-link"&gt;&lt;/i&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .='&lt;div class="post-date"&gt;&lt;div class="day"&gt;'.$post_day.'&lt;/div&gt;&lt;div class="month"&gt;'.$post_month.'&lt;/div&gt;&lt;div class="year"&gt;'.$post_year. '&lt;/div&gt;&lt;/div&gt;';
$output .= '&lt;div class="post-image-hover"&gt;&lt;/div&gt;';
$output .= '&lt;a href="'.$image.'" data-lightbox="example-set" class="icon zoom"&gt;&lt;/a&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="post-author"&gt;';
$output .= '&lt;div class="post_author1"&gt;'.$post_author.'&amp;nbsp;&amp;nbsp;&lt;/div&gt;';
/*if($comments-&gt;total_comments &gt; 0):
$output .='&lt;div class="comments-link"&gt;&lt;a href="'.get_permalink().'"&gt;'.$comments-&gt;total_comments.' comment &lt;/a&gt;&lt;/div&gt;';
else:
$output .='&lt;div class="comments-link"&gt;&lt;a href="'.get_permalink().'"&gt;Leave a comment &lt;/a&gt;&lt;/div&gt;';
endif;    */
$output .= '&lt;/div&gt;';
$output .= '&lt;div class="post-content-inner"&gt;';
$shorttitle = substr(get_the_title('','',FALSE),0,50);
$output .= '&lt;div class="post-title"&gt;&lt;a href="'.get_permalink().'" title="'.get_the_title().'"&gt;'.$shorttitle.'&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;div class="post-description"&gt;'.templatemela_blog_post_excerpt(18).'&lt;/div&gt;';
/*if ( comments_open() &amp;&amp; ! is_single() ) :
$args = array(
'status' =&gt; 'approved',
'number' =&gt; '5',
'post_id' =&gt; get_the_ID()
);
$comments = wp_count_comments(get_the_ID());
if($comments-&gt;total_comments == 0)
$text = 'Leave a comment';
if($comments-&gt;total_comments == 1)
$text = $comments-&gt;total_comments.' Comment';
if($comments-&gt;total_comments &gt; 1)
$text = $comments-&gt;total_comments.' Comments';
$output .= '&lt;span class="comments-link"&gt; &lt;i class="fa fa-comment"&gt;&lt;/i&gt;'.$text.'&lt;/span&gt;';
endif;*/


$output .= '&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;';
$i++;
endwhile;
wp_reset_postdata();
$output .=    '&lt;/div&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="no-result"&gt;No results found...&lt;/div&gt;';
endif;
return $output;
}
add_shortcode('blog_posts', 'shortcode_blog_posts_container');

/***************** Latest News Posts ****************/

function shortcode_latest_news_container($atts, $content = null, $code) {
extract(shortcode_atts(array(
'type' =&gt; 'slider',
'items_per_column' =&gt; 1,
'number_of_posts' =&gt; 10,
'category' =&gt; '',
'align' =&gt; 'center',
'width' =&gt; '100%'
), $atts));

$i = 1;
wp_reset_postdata();
$args = array(
'posts_per_page' =&gt; $number_of_posts,
'post_status' =&gt; 'publish',
'category' =&gt; $category,
'orderby' =&gt; 'date'
);

$output = '';
$news_array = new WP_Query( $args );

if ( $news_array-&gt;have_posts() ):
$output .= '&lt;div id="latest-news-products" class="latest-news-content" style="width:'.$width.'"&gt;';
if($type == "slider") {
$output .= '&lt;div id="'.$items_per_column.'_latest_news_carousel" class="latest-news-carousel"&gt;';
} else {
$output .= '&lt;div id="latest_news_grid" class="latest-news-grid latest-news-cols-'.$items_per_column.'"&gt;';
}

while ( $news_array-&gt;have_posts() ) : $news_array-&gt;the_post();

if($i % $items_per_column == 1 )
$class = " first";
elseif($i % $items_per_column == 0 )
$class = " last";
else
$class = "";
if ( has_post_thumbnail() &amp;&amp; ! post_password_required() ) :
$post_thumbnail_id = get_post_thumbnail_id();
$image = wp_get_attachment_url( $post_thumbnail_id );
else:
$image = get_template_directory_uri()."/images/placeholders/placeholder.jpg";
endif;
$src = mr_image_resize($image, 150, 150, true, 't', false);
if( empty ( $src ) || $src == 'image_not_specified' ):
$src = get_template_directory_uri()."/images/megnor/placeholder.png";
$src = mr_image_resize($src, 150, 150, true, 't', false);
endif;
$output .= '&lt;div class="item single-post-container'.$class.' '.$align.'"&gt;';
$output .= '&lt;div class="single-post"&gt;';
$output .= '&lt;div class="post-image"&gt;';
$output .= '&lt;img src="'.$src.'" title="'.get_the_title().'" alt="'.get_the_title().'" /&gt;';
$output .= '&lt;div class="post-image-hover"&gt;&lt;/div&gt;';
$output .= '&lt;a href="'.$image.'" data-lightbox="example-set" class="icon zoom"&gt;&lt;/a&gt;';

$output .= '&lt;/div&gt;';
$shorttitle = substr(get_the_title('','',FALSE),0,50);
$output .= '&lt;div class="post-title"&gt;&lt;a href="'.get_permalink().'" title="'.get_the_title().'"&gt;'.$shorttitle.'&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;div class="post-description"&gt;'.templatemela_blog_post_excerpt(25).'&lt;/div&gt;';
$output .= '&lt;div class="post-date"&gt;'.date("j M, Y", strtotime(get_the_date())).'&lt;/div&gt;';
$output .= '&lt;/div&gt;&lt;/div&gt;';
$i++;
endwhile;
wp_reset_postdata();
$output .=    '&lt;/div&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="no-result"&gt;No results found...&lt;/div&gt;';
endif;
return $output;
}
add_shortcode('latest_news', 'shortcode_latest_news_container');

/***************** Google Map ****************/

function tm_mapshortcode( $atts, $content = null )
{
extract( shortcode_atts( array(
'latlong' =&gt; '-33.86938,151.204834',
'icon' =&gt; get_template_directory_uri().'/images/megnor/map-pin.png',
'height' =&gt; '400',
'id' =&gt; '0'
), $atts ) );

$text = preg_replace('#^&lt;\/p&gt;|&lt;p&gt;$#', '', do_shortcode($content));

return tm_googleMap($latlong, $text, $icon, $height, 1, '');

}
add_shortcode('tm_map', 'tm_mapshortcode');


/***************** Addess ****************/
function shortcode_address($atts, $content = null)
{
extract(shortcode_atts(array(
'title' =&gt; '',
'description' =&gt; '',
'address_label' =&gt; 'Address:',
'phone_label' =&gt; 'Phone numbers:',
'phone' =&gt; '',
'email_label' =&gt; 'Email:',
'email' =&gt; '',
'email_link' =&gt; '',
'other_label' =&gt; 'We are open:',
'other' =&gt; '',

), $atts));
$output = '';
$output .= '&lt;div class="address-container hb-animate-element right-to-left"&gt;';
if(!empty($title))
$output .= '&lt;h1 class="address-title simple-title"&gt;&lt;span&gt;'.$title.'&lt;/span&gt;&lt;/h1&gt;';
if(!empty($description))
$output .= '&lt;div class="address-description description"&gt;'.$description.'&lt;/div&gt;';

/*$output .= '&lt;div class="address-label"&gt;'.$address_label.'&lt;/div&gt;';*/
$output .= '&lt;div class="address-text"&gt;&lt;i class="fa fa-map-marker"&gt;&lt;/i&gt;'.do_shortcode($content).'&lt;/div&gt;';

if(!empty($phone)):
/*$output .= '&lt;div class="address-label"&gt;'.$phone_label.'&lt;/div&gt;';*/
$output .= '&lt;div class="address-text"&gt;&lt;i class="fa fa-phone"&gt;&lt;/i&gt;'.$phone.'&lt;/div&gt;';
endif;

if(!empty($email)):
/*$output .= '&lt;div class="address-label"&gt;'.$email_label.'&lt;/div&gt;';*/
if(!empty($email_link)):
$output .= '&lt;div class="address-text"&gt;&lt;i class="fa fa-envelope "&gt;&lt;/i&gt;&lt;a herf="'.$email_link.'"&gt;'.$email.'&lt;/a&gt;&lt;/div&gt;';
else:
$output .= '&lt;div class="address-text&gt;&lt;i class="fa fa-envelope "&gt;&lt;/i&gt;'.$email.'&gt;&lt;/div&gt;';
endif;
endif;
if(!empty($other)):
/*$output .= '&lt;div class="address-label"&gt;'.$other_label.'&lt;/div&gt;';*/
$output .= '&lt;div class="address-text"&gt;&lt;i class="fa fa-info"&gt;&lt;/i&gt;'.$other.'&lt;/div&gt;';
endif;
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_address', 'shortcode_address');

/***************** Static links ****************/

function shortcode_link($atts, $content = null)
{
extract(shortcode_atts(array(
'link_url' =&gt;  '',
), $atts));
$output = '';
if(!empty($link_url))
$output .= '&lt;li&gt;&lt;a href="'.$link_url.'"&gt;'.do_shortcode($content).'&lt;/a&gt;&lt;/li&gt;';
else
$output .= '&lt;li&gt;'.do_shortcode($content).'&lt;/li&gt;';
return $output;
}
add_shortcode('link', 'shortcode_link');


function shortcode_tm_links($atts, $content = null)
{
extract(shortcode_atts(array(
), $atts));
$output = '';
$output .= '&lt;ul class="links"&gt;';
$output .= do_shortcode($content);
$output .=    '&lt;/ul&gt;';
return $output;
}
add_shortcode('tm_links', 'shortcode_tm_links');

/***************** H family ****************/

function shortcode_h1($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h1&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h1&gt;';
return $output;
}
add_shortcode('tm_h1', 'shortcode_h1');

function shortcode_h2($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h2&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h2&gt;';
return $output;
}
add_shortcode('tm_h2', 'shortcode_h2');

function shortcode_h3($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h3&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h3&gt;';
return $output;
}
add_shortcode('tm_h3', 'shortcode_h3');

function shortcode_h4($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h4&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h4&gt;';
return $output;
}
add_shortcode('tm_h4', 'shortcode_h4');

function shortcode_h5($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h5&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h5&gt;';
return $output;
}
add_shortcode('tm_h5', 'shortcode_h5');

function shortcode_h6($atts, $content = null) {

extract(shortcode_atts(array(
), $atts));

$output = '';
$output .= '&lt;h6&gt;';
$output .=    do_shortcode($content);
$output .=    '&lt;/h6&gt;';
return $output;
}
add_shortcode('tm_h6', 'shortcode_h6');

/*============== All Boxes ==================*/

function shortcode_successbox($atts, $content=null, $code="") {
$return = '&lt;div class="success-message message"&gt;';
$return .= $content;
$return .= '&lt;/div&gt;';
return $return;
}
add_shortcode('tm_success' , 'shortcode_successbox' );

function shortcode_errorbox($atts, $content=null, $code="") {
$return = '&lt;div class="error-message message"&gt;';
$return .= $content;
$return .= '&lt;/div&gt;';
return $return;
}
add_shortcode('tm_error' , 'shortcode_errorbox' );

function shortcode_messagebox($atts, $content=null, $code="") {
$return = '&lt;div class="message-message message"&gt;';
$return .= $content;
$return .= '&lt;/div&gt;';
return $return;
}
add_shortcode('tm_message' , 'shortcode_messagebox' );

function shortcode_warningbox($atts, $content=null, $code="") {
$return = '&lt;div class="warning-message message"&gt;';
$return .= $content;
$return .= '&lt;/div&gt;';
return $return;
}
add_shortcode('tm_warning' , 'shortcode_warningbox' );

/***************** Products ****************/

function shortcode_woo_products_container($atts, $content = null, $code) {
global $logotype;
extract(shortcode_atts(array(
'type' =&gt; 'grid',
'items_per_column' =&gt; 3,
'product' =&gt; 'shop'
), $atts));

$logotype = $type;

$output = '';
$output .= '&lt;div id="woo-products" class="woo-content products_block '.$product.'"&gt;';

if($type == "slider") {
$output .= '&lt;div id="'.$items_per_column.'_woo_carousel" class="woo-carousel"&gt;';
} else {
$output .= '&lt;div id="woo_grid" class="woo-grid cols-'.$items_per_column.'"&gt;';
}
$output .=    do_shortcode($content).'&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('woo_products', 'shortcode_woo_products_container');

/******************* WooCommerce Small Prodcuts ******/
function shortcode_woo_small_products_container($atts, $content = null, $code) {
global $logotype;
extract(shortcode_atts(array(
'type' =&gt; 'grid',
'items_per_column' =&gt; 2,
), $atts));

$logotype = $type;

$output = '';
$output .= '&lt;div id="woo-small-products" class="woo-content products_block"&gt;';

if($type == "slider") {
} else {
$output .= '&lt;div id="woo_grid" class="woo-grid cols-'.$items_per_column.'"&gt;';
}
$output .=    do_shortcode($content).'&lt;/div&gt;&lt;/div&gt;';
return $output;
}
add_shortcode('woo_small_products', 'shortcode_woo_small_products_container');


function shortcode_cms_text($atts, $content = null, $code) {
extract(shortcode_atts(array(
'icon' =&gt; 'fa-arrows-alt',
'link_text' =&gt; '',
'link_url' =&gt; '',
'border' =&gt; 'yes',
'color' =&gt;'',
), $atts));

$output = '';
$variables = '';

if(!empty($border)):
$variables .= 'border-right:1px solid #'.$color.'';
endif;
$output .= '&lt;div class="cmstext" style="'.$variables.'"&gt;';
$output .= '&lt;div class="icon"&gt;&lt;i class="cms-icon fa '.$icon.'" &gt;&lt;/i&gt; &lt;/div&gt;';
$output .= '&lt;a href="'.$link_url.'"&gt;'.$link_text.'&lt;/a&gt;';
$output .= '&lt;/div&gt;';

return $output;
}
add_shortcode('tm_cms_text', 'shortcode_cms_text');

/*=============CMS Banner ============ */
function shortcode_cmsbanner($atts, $content = null)
{
extract(shortcode_atts(array(
'background_image' =&gt; '',
'background_repeat' =&gt; 'no-repeat',
'text1' =&gt; '',
'text2' =&gt; '',
"border_color"=&gt; 'ffffff',
"padding" =&gt; '10px',
"border" =&gt; '',
'margin' =&gt;    '',
), $atts));

$variables  = '';
$output = '';

if(!empty($background_image))
$variables .= 'background-image: url('.$background_image.');';
$variables .= 'background-repeat:'.$background_repeat.';';
if($border == 'yes')
{
$variables .= 'border-left:1px solid #'.$border_color.';';
$variables .= 'border-right:1px solid #'.$border_color.';';
}
$variables .= 'padding:'.$padding.';';
$variables .= 'margin:'.$margin.';';

$output .= '&lt;div class="cms-container center" style="'.$variables.'"&gt;';

$output .= '&lt;div class="cms-content"&gt;';
$output .= '&lt;div class="cms-content-inner"&gt;';
$output .= '&lt;div class="cms-title"&gt;&lt;a href="'.$link_url.'" class="text1"&gt;'.$text1.'&lt;/a&gt;&lt;a class="text2"&gt;'.$text2.'&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('cmsbanner', 'shortcode_cmsbanner');

/*=============Sub Banner ============ */
function shortcode_subbanner($atts, $content = null)
{
extract(shortcode_atts(array(
'image'    =&gt; '',
'padding' =&gt; '',
'margin' =&gt; '',
'height' =&gt; '',
'width' =&gt; '',

), $atts));

$variables  = '';
$output = '';

if(!empty($image)) :
$variables .= 'padding:'.$padding.';';
$variables .= 'margin:'.$margin.';';
endif;

$output .= '&lt;div class="sub-container center" style="'.$variables.'"&gt;';
$output .= '&lt;div class="inner-image"&gt;&lt;a href="'.$link_url.'" target="_Blank"&gt;&lt;img src='.$image.' height="'.$height.'" width="'.$width.'"&gt;&lt;/a&gt;&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('subbanner', 'shortcode_subbanner');



function shortcode_cms_banner($atts, $content = null)
{
extract(shortcode_atts(array(
'background_img' =&gt; '',
'background_color' =&gt; '',
'background_repeat' =&gt; 'no-repeat',
'image' =&gt; '',
'maintitle' =&gt; '',
'subtitle' =&gt; '',
), $atts));

if($backgroung_img != NULL) {
$get_imagepath = $backgroung_img;
} else {
$get_imagepath = get_template_directory_uri() . '/images/megnor/no_image.jpg';
}

$output = '';
$variables = '';
if(!empty($background_img)):
$variables .= 'background-image: url('.$background_img.');';
$variables .= 'background-color:#'.$background_color.';';
$variables .= 'background-repeat:'.$background_repeat.';';
endif;
$output .='&lt;div class ="tm_cms_banner column1" style="'.$variables.');"&gt;';
$output .= '&lt;div class ="cms-image"&gt;&lt;img src="'.$image.'"&gt;&lt;/div&gt;';
$output .='&lt;div class ="tm_cms_banner_inner"&gt;';
$output .='&lt;div class = "maintitle"&gt;'.$maintitle.'&lt;/div&gt;';
$output .='&lt;div class = "subtitle"&gt;'.$subtitle.'&lt;/div&gt;';
$output .='&lt;/div&gt; &lt;/div&gt;';

return $output;
}
add_shortcode('tm_cms_banner', 'shortcode_cms_banner');

/*=============Latest Product Information============ */

function shortcode_information($atts, $content = null) {
extract(shortcode_atts(array(
'title' =&gt; '',
'description' =&gt; '',
), $atts));

$output = '';
$output    .= '&lt;div class="information"&gt;';
$output .= '&lt;div class="info-title"&gt;' .$title. '&lt;/div&gt;';
$output    .= '&lt;div class="info-description"&gt;' .$description. '&lt;/div&gt;';
$output    .= '&lt;/div&gt;';
return $output;
}
add_shortcode("information", "shortcode_information");


function shortcode_product_tabs($atts, $content = null)
{
extract(shortcode_atts(array(
'tab1_text' =&gt; '',
'tab2_text' =&gt; '',
'tab3_text' =&gt; '',
), $atts));

$output = '';

$output .= '&lt;div id="horizontalTab"&gt;';
$output .= '&lt;ul class="resp-tabs-list"&gt;';
$output .= '&lt;li class="hb-animate-element top-to-bottom"&gt;'.$tab1_text. '&lt;/li&gt;';
$output .= '&lt;li class="hb-animate-element top-to-bottom"&gt;'.$tab2_text. '&lt;/li&gt;';
$output .= '&lt;li class="hb-animate-element top-to-bottom"&gt;'.$tab3_text. '&lt;/li&gt;';
$output .= '&lt;/ul&gt;';
$output .= '&lt;div class="resp-tabs-container"&gt;';
$output .= do_shortcode($content);
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('tm_product_tabs', 'shortcode_product_tabs');


/***** Product Category Tabs List******/
function shortcode_woo_category_slider($atts, $content = null, $code) {
extract(shortcode_atts(array(
'category_ids' =&gt; '95,105,102,103',
'items_per_column' =&gt; '4',
), $atts));

$category_ids_array = explode(",",$category_ids);
$category_ids_array[] = $category_ids_array;

$output = '';
$output .= '&lt;div id="categorytab"&gt;';
$category_ids = '';
$term_category_id = '';
$term_category_name = '';
$term_categroy_slug = '';
$term_thumbnai_id = '';
$term_image = '';
$output .= '&lt;ul class="resp-tabs-list"&gt;';
foreach($category_ids_array as $key){
$category_ids = get_term( $key, 'product_cat' );
if($category_ids){
$term_category_id = $category_ids-&gt;term_id;
$term_category_name = $category_ids-&gt;name;
$term_category_slug = $category_ids-&gt;slug;
$term_thumbnail_id =  get_woocommerce_term_meta( $term_category_id , 'thumbnail_id', true );
$term_image = wp_get_attachment_url( $term_thumbnail_id );  // get the image URL
$output .= '&lt;li&gt;'.$term_category_name.'&lt;/li&gt;';
}
}
$output .= '&lt;/ul&gt;';
$output .= '&lt;div class="resp-tabs-container"&gt;';
foreach($category_ids_array as $key){
$term_array = get_term( $key, 'product_cat' );
$term_category_id = $term_array-&gt;term_id;
$term_category_slug = $term_array-&gt;slug;
$output .= do_shortcode('[woo_products type="grid" items_per_column="4"][product_category category="'.$term_category_slug.'"][/woo_products]');
}
$output .= '&lt;/div&gt;';
$output .= '&lt;/div&gt;';
return $output;
}
add_shortcode('woo_categories', 'shortcode_woo_category_slider');
//deactivate WordPress function
remove_shortcode('gallery', 'gallery_shortcode');

//activate own function
add_shortcode('gallery', 'msdva_gallery_shortcode');
function msdva_gallery_shortcode($attr) {
$post = get_post();

static $instance = 0;
$instance++;

if ( ! empty( $attr['ids'] ) ) {
// 'ids' is explicitly ordered, unless you specify otherwise.
if ( empty( $attr['orderby'] ) )
$attr['orderby'] = 'post__in';
$attr['include'] = $attr['ids'];
}

// Allow plugins/themes to override the default gallery template.
$output = apply_filters('post_gallery', '', $attr);
if ( $output != '' )
return $output;

// We're trusting author input, so let's at least make sure it looks like a valid orderby statement
if ( isset( $attr['orderby'] ) ) {
$attr['orderby'] = sanitize_sql_orderby( $attr['orderby'] );
if ( !$attr['orderby'] )
unset( $attr['orderby'] );
}

extract(shortcode_atts(array(
'order' =&gt; 'ASC',
'orderby' =&gt; 'menu_order ID',
'id' =&gt; $post ? $post-&gt;ID : 0,
'itemtag' =&gt; 'dl',
'icontag' =&gt; 'dt',
'captiontag' =&gt; 'dd',
'divtag' =&gt; 'div',
'columns' =&gt; 3,
'size' =&gt; 'full',
'include' =&gt; '',
'exclude' =&gt; '',
'link' =&gt; 'file' // CHANGE #1
), $attr, 'gallery'));

$id = intval($id);
if ( 'RAND' == $order )
$orderby = 'none';

if ( !empty($include) ) {
$_attachments = get_posts( array('include' =&gt; $include, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );

$attachments = array();
foreach ( $_attachments as $key =&gt; $val ) {
$attachments[$val-&gt;ID] = $_attachments[$key];
}
} elseif ( !empty($exclude) ) {
$attachments = get_children( array('post_parent' =&gt; $id, 'exclude' =&gt; $exclude, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
} else {
$attachments = get_children( array('post_parent' =&gt; $id, 'post_status' =&gt; 'inherit', 'post_type' =&gt; 'attachment', 'post_mime_type' =&gt; 'image', 'order' =&gt; $order, 'orderby' =&gt; $orderby) );
}

if ( empty($attachments) )
return '';

if ( is_feed() ) {
$output = "\n";
foreach ( $attachments as $att_id =&gt; $attachment )
$output .= templatemela_wp_get_attachment_link($att_id, $size, true) . "\n";
return $output;
}

$itemtag = tag_escape($itemtag);
$captiontag = tag_escape($captiontag);
$icontag = tag_escape($icontag);
$valid_tags = wp_kses_allowed_html( 'post' );
if ( ! isset( $valid_tags[ $itemtag ] ) )
$itemtag = 'dl';
if ( ! isset( $valid_tags[ $captiontag ] ) )
$captiontag = 'dd';
if ( ! isset( $valid_tags[ $icontag ] ) )
$icontag = 'dt';

$columns = intval($columns);
$itemwidth = $columns &gt; 0 ? floor(100/$columns) : 100;
$float = is_rtl() ? 'right' : 'left';

$selector = "gallery-{$instance}";

$gallery_style = $gallery_div = '';
if ( apply_filters( 'use_default_gallery_style', true ) )
$gallery_style = "
&lt;style type='text/css'&gt;
#{$selector} {
margin: auto;
}
#{$selector} .gallery-item {
float: {$float};
margin-top: 10px;
text-align: center;
width: {$itemwidth}%;
}
#{$selector} img {
border: 2px solid #cfcfcf;
}
#{$selector} .gallery-caption {
margin-left: 0;
}
/* see gallery_shortcode() in wp-includes/media.php */
&lt;/style&gt;";
$size_class = sanitize_html_class( $size );
$gallery_div = "&lt;div id='$selector' class='gallery galleryid-{$id} gallery-columns-{$columns} gallery-size-{$size_class}'&gt;";
$output = apply_filters( 'gallery_style', $gallery_style . "\n\t\t" . $gallery_div );

$i = 0;

foreach ( $attachments as $id =&gt; $attachment ) {
$image_url = $attachment-&gt;guid;
$image_output = templatemela_wp_get_attachment_link( $id, $size, true, false );
$image_meta = wp_get_attachment_metadata( $id );

$orientation = '';
if ( isset( $image_meta['height'], $image_meta['width'] ) )
$orientation = ( $image_meta['height'] &gt; $image_meta['width'] ) ? 'portrait' : 'landscape';
$output .= "&lt;{$itemtag} class='gallery-item'&gt;";
$output .= "
&lt;{$icontag} class='gallery-icon {$orientation}'&gt;
$image_output
&lt;/{$icontag}&gt;";
$output .= "
&lt;{$captiontag} class='wp-caption-text gallery-caption'&gt;
&lt;{$divtag} class='gallery-caption-inner'&gt;";

$output .= " &lt;{$divtag} class='wp-caption-text gallery-title'&gt;
" . wptexturize($attachment-&gt;post_title) . "
&lt;/{$divtag}&gt;";

if ( $captiontag &amp;&amp; trim($attachment-&gt;post_excerpt) ) {
$output .= "&lt;{$divtag} class='wp-caption-text gallery-excerpt'&gt;";
if($columns == 1):
$excerpt_length = 100;
elseif($columns == 2):
$excerpt_length = 300;
elseif($columns == 3):
$excerpt_length = 200;
elseif($columns == 4):
$excerpt_length = 50;
elseif($columns == 5):
$excerpt_length = 10;
endif;
$output .= substr($attachment-&gt;post_excerpt,0,$excerpt_length);
$output .= "&lt;/{$divtag}&gt;";

$output .= "&lt;{$divtag} class='wp-caption-text gallery-zoom'&gt;
&lt;a href=" . $image_url . " title='Click to view Full Image' class='icon mustang-gallery'&gt;&lt;i class='fa fa-search'&gt;&lt;/i&gt;&lt;/a&gt;
&lt;/{$divtag}&gt;";

$output .= "&lt;{$divtag} class='wp-caption-text gallery-redirect'&gt;
&lt;a href=" . get_attachment_link( $attachment-&gt;ID ) . " title='Click to view Read More' class='icon readmore'&gt;&lt;i class='fa fa-share'&gt;&lt;/i&gt;&lt;/a&gt;
&lt;/{$divtag}&gt;";
}else{

$output .= "&lt;{$divtag} class='wp-caption-text gallery-zoom no-text'&gt;
&lt;a href=" . $image_url . " title='Click to view Full Image' class='icon mustang-gallery'&gt;&lt;i class='fa fa-search'&gt;&lt;/i&gt;&lt;/a&gt;
&lt;/{$divtag}&gt;";
$output .= "&lt;{$divtag} class='wp-caption-text gallery-redirect'&gt;
&lt;a href=" . get_attachment_link( $attachment-&gt;ID ) . " title='Click to view Read More' class='icon readmore'&gt;&lt;i class='fa fa-share'&gt;&lt;/i&gt;&lt;/a&gt;
&lt;/{$divtag}&gt;";
}
$output .= "&lt;/{$divtag}&gt;";
$output .= "&lt;/{$captiontag}&gt;";
$output .= "&lt;/{$itemtag}&gt;";
}

$output .= "
&lt;/div&gt;\n";

return $output;
}


function templatemela_wp_get_attachment_link( $id = 0, $size = 'thumbnail', $permalink = true, $icon = false, $text = false ) {
$id = intval( $id );
$_post = get_post( $id );
if ( empty( $_post ) || ( 'attachment' != $_post-&gt;post_type ) || ! $url = wp_get_attachment_url( $_post-&gt;ID ) )
return __( 'Missing Attachment', 'templatemela' );

if ( $permalink )
// $url = get_attachment_link( $_post-&gt;ID ); // we want the "large" version!!
// FIX!! ask for large URL
$image_attributes = wp_get_attachment_image_src( $_post-&gt;ID, 'large' );
$url = $image_attributes[0];
// $url = wp_get_attachment_image( $_post-&gt;ID, 'large' );

$post_title = esc_attr( $_post-&gt;post_title );

if ( $text )
$link_text = $text;
elseif ( $size &amp;&amp; 'none' != $size )
$link_text = wp_get_attachment_image( $id, $size, $icon );
else
$link_text = '';

if ( trim( $link_text ) == '' )
$link_text = $_post-&gt;post_title;
return apply_filters( 'wp_get_attachment_link', "&lt;span rel='gallery-nr'&gt;$link_text&lt;/span&gt;", $id, $size, $permalink, $icon, $text );
}
?&gt;]Accordion[/title]
[tm_code][ tm_accordion style="1" ]
[ accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. [ /accordion]
[ accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. [ /accordion ]
[ accordion title="Nam tempor diam elit" ]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. [ /accordion ]
[ /tm_accordion ][/tm_code][/container]
<h3 class="widget-title">Style One and Two Accordion</h3>
[container padding="10px 0"]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style One Accordion[/title]
[tm_accordion style="1"]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion][/tm_accordion]
[/one_half]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Two Accordion[/title]
[tm_accordion style="2"]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion][/tm_accordion]
[/one_half]
[/container]
<h3 class="widget-title">Style Three and Four Accordion</h3>
[container padding="20px 0"]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Three Accordion[/title]
[tm_accordion style="3"]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[/tm_accordion]
[/one_half]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Four Accordion[/title]
[tm_accordion style="4"]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[accordion title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/accordion]
[/tm_accordion]
[/one_half]
[/container]
<h3 class="widget-title">Toggle Code</h3>
[container padding="10px 0"][title size="small" align="center" classname="sub_title"]Toggle[/title]
[tm_code][ tm_toggle style="1" ]
[ toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. [ /toggle]
[ toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. [ /toggle ]
[ toggle title="Nam tempor diam elit" ]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. [ /toggle ]
[ /tm_toggle ][/tm_code][/container]
<h3 class="widget-title">Style One and Two Toggle</h3>
[container padding="20px 0"]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style One Toggle[/title]
[tm_toggle style="1"]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[/tm_toggle]
[/one_half]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Two Toggle[/title]
[tm_toggle style="2"]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[/tm_toggle]
[/one_half]
[/container]
<h3 class="widget-title">Style Three and Four Toggle</h3>
[container padding="20px 0"]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Three Toggle[/title]
[tm_toggle style="3"]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[/tm_toggle]
[/one_half]
[one_half content_width="95%"]
[title size="small" type="simple" classname="sub_title"]Style Four Toggle[/title]
[tm_toggle style="4"]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[toggle title="Nam tempor diam elit"]Nunc molestie dolor nec magna fermen atum in pharetra orci mollis. Nam tempor diam elit. Praesent magna metus, conse viverra nec, convallis et lacus. [/toggle]
[/tm_toggle]
[/one_half]
[/container]