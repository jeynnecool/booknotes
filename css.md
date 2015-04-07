# Css Mastery

**date: 20140718-15:55**

**tags: css**

**Advanced Web Standards Solutions**

**author: Andy Buddy, Cameron Moll, and Simon Collison**

# 1. Setting the foundation

XHTML :: Extensible Hypertext Markup Language.

(X)HTML :: both XHTML and HTML.

Meaningful markup
 - easier to work with.
 - easy for humans to understand. meaningful markup, also known as semantic markup, can be understood by programs and other devices.
 - provides you with a simple way of targeting the elements you wish to style.

(X)HTML includes variety of meaningful elements, such as:
 - h1, h2, etc.
 - ul, ol and dl
 - strong and em
 - blockquote and cite
 - abbr, acronym, and code
 - fieldset, legend and label
 - caption, thead, tbody and tfoot

### IDs and classes

ID :: used to identify an individual element on page, and **must be unique**. They are also useful to identifying one-off elements. ID names should be applied to conceptually similar elements in order to avoid confusion. 


class :: the class name can be applied to any number of elements on a page. Useful for identifying types of content or similar items.


Naming IDs and classes
 -  important to keep the name as meaningful and "un-presentational" as possible.
 - case sensitivity. CSS is generally case sensitive, however, those elements appear in the markup, such as class and ID names, depends on the case sensitivity of the markup language.
 - don't overused or even abuse. Need to get fine-grained control over the style. classitis.


### Divs and spans

div :: stands for division and provides a way of dividing a document into meaningful areas. Only use `div` element if there is no existing element that will do the job. Using many divs is often described as *divitus* and is usually a sign that your code is poorly structured and overly complicated. group block-level elements.

span :: group or identify inline elements. 


### Document types, DOCTYPE switching, and browser modes

DTD :: a document type definition (DTD) is a set of machine-readable rules that define what is and isn't allowed in a particular version of XML or (X)HTML.

DOCTYPE :: a DOCTYPE declaration is a line or two of code at the start of your (X)HTML document that describes the particular DTD being used.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

Check if your (X)HTML is valid by using the W3C validator, or a plug-in like the Firefox Developer Extension. Important to help you track down bugs in your code.

validation tools 
 - http://validator.w3.org/
 - Firefox plug-in: Web Developers Extension plug-in.
 - developer tools for IE6.

Browser Mode 

the most obvious example of difference between these modes revolves around the IE on Windows proprietary box model. 

DOCTYPE switching :: is a hack used by browsers to distinguish legacy documents from more standards-compliant ones. It's important to include a fully formed DOCTYPE declaration on every page of your site and choose a strict DTD when using HTML.

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

//XML delaration
<?xml version="1.0" encoding="utf-8"?>
```


### Target elements

##### Common selector

Type selectors are used to target a particular type of element, such as a paragraph, an anchor, or a heading element. also referred to as *element* or *simple* selector.

`h1 {font-weight: bold;}`

Descendant selectors allow you to target the descendant of a particular element or group of elements.

`li a {text-decoration: none;}`

Combination of type, descendant, ID, and/or class selectors

```css
#mainContent h1 {font-size: 1.8em;}
#secondaryContent h1 {font-size: 1.2em;}
```

##### Pseudo-classes

`:link` and `:visited` are know as *link* pseudo-classes and can only applied to anchor elements. `:hover` and `:focus` are know as *dynamic* pseudo-classes, and can theoretically be applied to any elements. Unfortunately, only a few modern browsers such as Firefox support this functionality. IE 6 and below only pays attention to `:active` and `:hover` selectors if applied to an anchor link, and ignores `:focus` completely.


##### Universal selector 

acts like a wildcard, matching all the available elements. 


##### Advanced selectors

Child and adjacent sibling selectors

```html
#nav > li {font-weight: bold;}

<ul id="nav">
<li>Home</li>
<li>Services
<ul>
<li>Design</li>
<li>Development</li>
<li>Consultancy</li>
</ul>
</li>
<li>Contact Us </li>
</ul>
```

It is possible to "fake" a child selector that works in IE 6 and below by using the universal selector. To do this you first apply to all of the descendants the style you want the children to have. You then use the universal selector to override these styles on the children's descendants. So to fake the previous child selector example you would do this:

```css
#nav li {font-weight: bold;}
#nav li * {font-weight: normal;}
```

Adjacent sibling selector :: allows you to target an element that is preceded by another element that shares the same parent.

```html
h1 + p {font-weight: bold;}

<h1>Main Heading</h1>
<p>First Paragraph</p>
<p>Second Paragraph</p>
```

Attribute selector :: allows you to target an element based on the existence of an attribute or the attribute’s value.

```
<abbr title="Cascading Style Sheets">CSS</abbr>

abbr[title] {border-bottom: 1px dotted #999;}
abbr[title]:hover {cursor: help;}


//use rel attribute of nofollowing gain no added ranking benefit from Google.

a[rel="nofollow"] {
  background-image: url(nofollow.gif);
  padding-right: 20px;
}


//apply one style to IE and another style to more standards-complicant browser
//targeting the class attribute rather than using a class selector

.intro {border-style: solid;}
[class="intro"] {border-style: dotted;}


//use predefined keywords in the attribute of links to define the relationship one site owner has with another.

a[rel~="friend"] {background-image: url(friend.gif);}

<a href="http://www.hicksdesign.com/" rel="friend met colleague" >
John Hicks
</a>
```

Using `rel` attribute with friend value is known as XHTML Friends Network, or XFN for short, "microformats". 
 - http://gmpg.org/xfn/
 - http://microformats.org.



### Cascade and specificity

order of importance 

 - User styles flagged as !important
 - Author styles flagged as !important
 - Author style
 - User style 
 - Style applied by the browser/user agent


specificity

```
  form {width: 30em;}
  form#search {width: 15em;}
  form {}
```


make sure general styles are very general wihile specific styles are as specific as possible and never need to be overridden.

 
### Inheritance

don't confuse inheritance with the cascade.

certain properties, such as color or font-size, are inherited by the descendants of the elements those styles are applied to.


### Planning, organizing, and maintaining your stylesheets

add styles directly, or keep all the styles in on or more external stylesheets.

two ways to attach external stylesheets: link them or import them.

```html
<link href="/css/basic.css" rel="stylesheet" type="text/css" />

<style type="text/css">
  <!--
    @import url("/css/advanced.css");
  -->
</style>
```


### Commenting code

css comments start with `/*` and ends with `*/`.

structural comments

```
/*–––––––––––––––––––––––––––––––––––––––––––––––––
Basic Style Sheet (for version 4 browsers)
version: 1.1
author: andy budd
email: info@andybudd.com
website: xxxxx
–––––––––––––––––––––––––––––––––––––––––––––––––*/
```

note to self

```
/*
Use the star selector hack to give IE a different font size
.....
*/
```


### Remove comments and optimizing stylesheets

[online CSS optimizers](http://www.cssoptimiser.com/)

Some people have experimented with writing comments in PHP format and then serving their stylesheets up as PHP.

The best option is probably to enable server-side compression. if you are using Apache, talk to your host to install mod_gzip or mod_deflate. decompress file on the fly.

If you don’t have access to these Apache modules, you still may be able to
compress your files by following the tutorial found at http://www.fiftyfoureleven.com/weblog/web-development/css/the-definitive-css-gzip-method

### Style guide

I generally have one CSS file for **the basic style** and **another for typography and design embellishment**. This way, once the layout is set, I rarely have to go back and change the layout stylesheet. This also protects my layout stylesheet from accidentally being altered and breaking.


# 2. Visual Formatting Model Recap

Three of the most important CSS concepts to grasp are floating, positioning, and the box model.

### Box model

every element on the page is considered to be a rectangular box made up of the lement's content, padding, border and margin.

![css-mastery-01](/src/css-mastery-01.jpg)


IE/Win and the box model

![css-mastery-02](/src/css-mastery-02.jpg)

### Margin collapsing

when two or more vertical margins meet, they will collapse to form a single margin. The height of this margin will equal the height of the larger of the two collapsed margins.

![css-mastery-03](/src/css-mastery-03.jpg)

When one element is contained within another element, assuming there is no padding or border separating margins, their top and/or bottom margin will also collapse together.

![css-mastery-04](/src/css-mastery-04.jpg)

margin collapsing only happens with the vertical margins of block boxes in the normal flow of the document. Margins between inline boxes, floated, or absolutely positioned boxes never collapse.

### Positioning

##### visual formatting model

people often refer p, h1, or div as block-level elements. means they are elements that are visually displayed as blocks of content, or "block boxes".

elements such as strong or span are inline elements because their content is displayed within lines as "inline boxes".

cause an element to generate no box at all by setting its *display* property to none.

three basic positioning schemes in CSS
 - normal flow
 - floats
 - absolute positioning

Box-level boxes will appear vertically one after the other; the vertical distance between boxes is calculated by the boxes' vertical margins.

Inline boxes are laid out in a line horizontally. Their horizontal spacing can be adjusted using horizontal padding, borders, and margins. However, vertical padding, borders, and margins will have _no effect_ on the height of an inline box.

if add some block-level element, an anonymous block box is created even it has not been explicitly defined.

A similar thing happens with the lines of text inside a block-level element. A paragraph contains three lines of text, each line of text forms an anonymous line box.


##### Relative positioning

If you relatively position an element, it will stay exactly where it is.

```css
#myBox
{
  position: relative;
  left: 20px;
  top: 20px;
}
```

An absolutely positioned element is positioned in relation to its nearest positioned ancestor.

Relative positioning is "relative" to the element's initial position in the flow of the document, whereas absolute positioning is "relative" to nearest positioned ancestor or, if one doesn't exist, the initial container block.

absolutely positioned boxes are taken out of the flow of the document, they can overlap other elements on the page. control stacking order by setting =z-index=.

##### Fixed positioning

a fixed element's containing block is the viewport. This allows you to create floating elements that always stay at the same position in the window.

![css-mastery-05](/src/css-mastery-05.jpg)

![css-mastery-06](/src/css-mastery-06.jpg)


### Line boxes and clearing

cleared element's top margin to push the element's top border edge vertically down, past the float.

because the floated elements are taken out of the flow of the document, the wrapper div takes up no space. adding a clear div can solve the problem, but not the best. instead of clearing the floated text and image, you can choose to float the container div as well.

some people choose to float nearly everything in a layout and then clear those floats using an appropriate meaningful element, often the site footer. this helps reduce or eliminate the need for extraneous markup.

use the =:after= pseudo-class in combination with the content declaration to add new content at the end of the specified existing content.

```css
.clear:after
{
  content: ".";
  height: 0;
  visibility: hidden;
  display: block;
  clear: both;
}

/*this trick fails in IE6 and below.\*/

.clear {display: inline-block;}

/* Holly Hack Targets IE Win only \*/
* html .clear {height: 1%;}
.clear {display: block;}
/* End Holly Hack */
```


# Background Image and Image Replacement

default web browser behavior is to repeat background images horizontally and vertically.

Tiling images

creating a hook in html and applying the image using css

```css
#branding 
{
  width: 700px;
  height: 200px;
  background:url(/images/branding.gif) no-repeat;
}
```

creating a bullet using a background image

```css
h1
{
  padding-left: 30px;
  background: url(/images/bullet.gif) no-repeat left center;
}
```

![css-mastery-07](/src/css-mastery-07.jpg)

background positioning, percentage from the top left of the **parent element**.

You are not supposed to mix units such as pixels or percentage with keywords.

### Rounded-corner boxes

##### fixed-width rounded-corner boxes

three images, for backgroud, top and foot respectively.

![css-mastery-08](/src/css-mastery-08.jpg)

##### flexible rounded-corner box

four images, for top left, top right, bottom left, bottom right respectively.

![css-mastery-09](/src/css-mastery-09.jpg)

```html
<div class="box">
  <div class="box-outer">
    <div class="box-inner">
    <h2>Headline</h2>
    <p>Content</p>
    </div>
  </div>
</div>
```

### Mountaintop corners.

### Drop shadows

**Easy css drop shadows**

create the drop shadow graphic.

it is important to keep the code on one line and not separate the div and the image using whitespace. IE 5.5 has a whitespace bug that will cause a gap between the image and the drop shadow if your code is on separate lines.


**Drop shadows a la Clagnut**


**Fuzzy shadows**


### Image replacement

**image replacement**

Essentially you add your text to the document as normal, and then, using CSS, you hide the text and display a background image in its place. That way, search engines still have the HTML text to find, and the text will be available if you disable CSS.


##### Fahrner Image Replacement (FIR)

Wrap the text you want to replace in a span tag.

Then apply your replacement image as a background image to the heading element.

And hide the contents of the span by settings its display value to none.


##### Phark

put text inside element as normal, then apply a large negative =text-indent= (text indentation) to the headline.


##### Gilder/Levin method

one of the most robust way

add an addition, empty span inside the element you wish to replace. 

```
<h2>
  <span></span>Hello World
</h2>
```

set the dimensions of the element to equal the dimensions of your image, and set the position of the element to relative.

```css
h2
{
  width: 150px;
  height: 35px;
  position: relative;
}
```

set up a new positioning context for the enlosed span element. allowing you to position it absolutely over the text.
 
```css
h2 span
{
  background: url(hello_world.gif) no-repeat;
  position: absolute;
  width: 100%;
  height: 100%;
}
```


# 4. Styling Links
