---
title: Beaver Builder&#8217;s Mega Menu Extended
description: "Hello everybody. How are you doing?"
date: 2016-11-13
metadata:
  categories:
    - Beaver Builder
    - Website Building

tags: [ 'beaver-builder'] 
---
<iframe src="https://www.youtube.com/embed/TqgVe8-gH_I" width="1280" height="720" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

## Setting up a Beaver Builder Menu  
(only for Pro and above users)

Mega Menus were added to the Beaver Builder theme in version 1.5.  
Instructions on setting up a [Beaver builder Mega menu are here](http://kb.wpbeaverbuilder.com/article/139-set-up-a-mega-menu).  
Here are a couple of examples  with the default  mega-menu set ups:  
[PowerPack Demo](http://power.beaverjunction.com/)  
[Ultimate Addons Demo  
](http://ultimate.beaverjunction.com/)

[The example site in the video](http://only.beaverjunction.com/)

## Now to Extend Beaver Builder’s Mega Menu

As in the video above I make the Beaver Builder Mega Menu full width, add text, images and shortcodes. Shortcode are not recommended as they can conflict with the menus CSS styles and can slow sites more than using HTML.

## Makes Beaver Builder Mega Menu full width

This only creates the appearance of being full width with a CSS hack using a CSS pseudo element.  Add to the Beaver Builder Theme’s style.css file (at the bottom). Min-width is set to 768px the standard Beaver Builder setting. Adjust if changed.

```css
@media (min-width: 768px)
{
/\*This is just removing some default styles(not required)\*/
 .fl-page-nav UL.sub-menu
 {
 padding: 10px 0;
 -moz-box-shadow: none;
 -webkit-box-shadow: none;
 box-shadow: none;
 border: 0;
 background: none;
 }

 UL.navbar-nav LI.mega-menu> UL.sub-menu:after
 {
 content: "";
 display: block;
 position: absolute;
 left: 50%;
 top: -1px;
 height: 100%;
 width: 100vw;
 transform: translateX(-50%);
 z-index: -1;
 box-sizing: border-box;
 /\*These styles are replacing the BB style that are being over written above (not required)\*/
 border-top: 1px solid #DEDEDE;
 /\*+box-shadow: 0px 20px 20px rgba(0, 0, 0, 0.4);\*/
 -moz-box-shadow: 0px 20px 20px rgba(0, 0, 0, 0.4);
 -webkit-box-shadow: 0px 20px 20px rgba(0, 0, 0, 0.4);
 box-shadow: 0px 20px 20px rgba(0, 0, 0, 0.4);
 background-color: #F6F6F6;
 }
}
```

## Adds a description area to WordPress Menus

The following three snippet should be added the Beaver Builder Child Themes functions.php file. Add to the bottom if uncertain. Updated to work with Menu Modules.

```php
// adds descriptions to menus
function prefix\_nav\_description( $item\_output, $item, $depth, $args ) {
 if ( !empty( $item->description ) ) {
 $item\_output = str\_replace( $args->link\_after . '\</a>', '\<p class="menu-item-description">' . $item->description . '\</p>' . $args->link\_after . '\</a>', $item\_output );
 }
 
 return $item\_output;
}
add\_filter( 'walker\_nav\_menu\_start\_el', 'prefix\_nav\_description', 10, 4 );
```

### Allow HTML in the description area to WordPress Menus

```php
// Stop WP removing HTML in Menu description area


remove\_filter('nav\_menu\_description', 'strip\_tags');

add\_filter( 'wp\_setup\_nav\_menu\_item', 'cus\_wp\_setup\_nav\_menu\_item' );

function cus\_wp\_setup\_nav\_menu\_item($menu\_item) {

$menu\_item->description = apply\_filters( 'nav\_menu\_description', $menu\_item->post\_content );

return $menu\_item;

}
```

### Allows Shortcodes in the description areas

```php
// allows shortcodes in the menu 
//(not recommend as BB styling is often lost and it use more server resources than HTML)

add\_filter('wp\_nav\_menu', 'do\_menu\_shortcodes'); 
function do\_menu\_shortcodes( $menu\_item ){ 
 return do\_shortcode( $menu\_item ); 
}
```

## Finishing Touches

This next snippet stops non linking text from changing color when hovered over. It is set to black here.

```css
/\*this is placed in style.css to overwrite the CSS in the theme\*/
.fl-page-nav-wrap A:hover, .fl-page-nav-wrap A:focus, .fl-page-nav-wrap A:hover \*, .fl-page-nav-wrap A:focus \*, .fl-page-nav-wrap A.fa:hover, .fl-page-nav-wrap A.fa:focus
{
 color: #000000;
}
```

This to hides menu items you don’t want to show in your mobile navigation. You will need to add **mobile-nav-header** to the CSS of the menu item

```css
@media (max-width: 768px)
{
 UL.navbar-nav LI.mega-menu .mobile-nav-header>A
 {
 display: none;
 }
}
```