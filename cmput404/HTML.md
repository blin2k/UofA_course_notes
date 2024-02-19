# Standards
- WHATWG
	- HTML living standard
	- continually updated
	- constantly evolving
	- no version numbers
	- generally perfered
- W3C
	- HTML 5 standard
	- occasionally releases versions
	- versions: 5.0, 5.1, 5.2
	- best option when writing HTML is to use a reference with a compatibility table

# Start HTML
- start with `<!DOCTYPE html>`
	- tells the browser we are not using ancient HTMLs
- `<html>`
	- enclose your content in the HTML tag
- `<head>`
	- information about the webpage
	- usually include a `<title>` here
	- `<meta>`
		- contains meta information for browsers and other tools to help interpret
- `<body>`
	- information actually show up on the page
- `<tag>`
	- all tags should closed to allow for ease of reading and parsing, except void tags
	- `<this></this>`
	- lower case
	- `<voidtag>`
		- there are a list of void tags
		- `<voidtag/>`
			- IDE might not like it if you don't put `/>` at the end
		- `<br>`
			- line break
- `<p>`
	- paragraph
	- you can use CSS to style there text blocks
	- multiple whitespace like a combination of newline, tab, and space, doesn't matter
		- they will get collapsed to one single space
		- `<br>` is used to get newline
- `<img>`
	- use hyperlinks (URIs) to reference them and include them
	- `<img src="../images/plasma.png" alt="plasma pattern" width="30" height="60">`
		- `alt` tags is for machine and human-readable
- `<a>`
	- anchor tag
		- hyperlinks
	- let us link to other documents or locations
	- `href` attribute links to a URL (can be a relative location of the current page)
	- `<a href="http://ualberta.ca"> UofA site </a>`
	- `<a href="../">` relative link
- `<div>`
	- cause a line break before it
	- `<div style="font-size:150%"> example </div>`
- `<span>`
	- be in lined
	- should stay in `<div>`
	- `<span style="background-color: #001122; font-weight:bold"> example </span>`
- `<input>`
	- usually inside a `form`
	- type
		- text (default) <input>
		- file <input type='file'>
		- image <input type="image">
		- checkbox <input type="checkbox"> <input type="checkbox" checked>
		- date <input type="date">
		- radio <input type='radio'><input type='radio' checked>
		- submit <input type="submit">
		- range <input type="range" min='0' max='50'>
		- etc....
	- name
		- the name to send in the query string or post
	- value
		- default value
- `<select>`
	- also inside a form
	- <select><option value='this'>this</option><option value="that">that</option></select>
- `<form>`
	- method
		- specifies the HTTP method (POST / GET)
	- action
		- specifies the URI to GET or POST to
	- `<form action="https://localhost:8000/" method="get"> ... </form>`

## Cascading
Accumulation of CSS properties like color, font-weight, etc.
```html
<span style="color:#001122;">
	Hi
	<span style="font-weight:bold;">
		Hello
		<span style="box-shadow:10px 10px 5px #888888;">
			Aloha
		</span>
	</span>
</span>
```
All three words are blue,
the last two are bold,
the last one has a box shadow.
# XML
You can write HTML in XML format if you follow XHTML
- valid HTML is not valid XML
- valid XML is not valid HTML
"polyglot HTML" was meant to combine there two but was abandoned in 2015.

`<voidtag/>` syntax in HTML is still supported but breaks other HTML parsers.

XML is unforgiving
- simple mistake could cause a parser to refuse to parse the XML

# CSS
Cascading Style Sheets
- can be applied on a per tag level or globally

```html
<!-- 1. Include CSS file -->
<link href="path/to/cssfile.css" ref="stylesheet">

<!-- 2. or you can build a Inline style sheet -->
<style type="text/css">
	.angry{
		font-weight:900;
		zoom:3;
	}
	.angry:nth-child(odd){
		color:green;
		transform:retate(7deg);
		-webkit-transform:rotate(7deg);
		float: left;
	}
	.angry:nth-child(even){
		color:red;
		transform:retate(-12deg);
		-webkit-transform:rotate(-12deg);
		float: right;
	}
</style>

<p style="color:oringe"> Apply style directly </p>
<div>
	<div class="angry"> This is the odd one, will be displayed at the left </div>
	<div class="angry"> This is the even one, will be displayed at the right </div>
</div>
```

## Basic CSS
- color
	- `color:#001122`
	- `color:blue`
- font-family
	- `font-family:"Times New Roman"`
- font-size
	- `font-size:10px`
	- `font-size:10pt`
	- `font-size:large`
	- `font-size:200%`
- font-style
	- `font-style:normal`

## Background
```css
.bg1 { background-color:red }
.bg2 { background-color:#aabbcc}
.bg3 { background-img:url('../images/plasma.png'); }
```

```html
<p class="bg1"> red <\p>
<p class="bg2"> hex <\p>
<p class="bg3">
	examples<br>
	another one<br>
</p>
```
<p style="color: blue"> Blue </p>

---
## Selector
---
- `.class`
	- creates a class and specifies the styles
	- you can set the `class` attribute to select it

`.hightlight { background-color:yellow; }`
`<p class="highlight"> example </p>`

or combine it with tags to override

`p.highlight { background-color:yellow; }`

---
- `#id`
	- one to one
	- whereas `class` are one to multiple

`#yellowtag { background-color:yellow}`
`<p id="yellowtag"> example </p>`

---
- `element`
	- style entire HTML elements
	- theme all `div` or `img` or `link`

`p { background-color:blue }`
`<p> example </p>`

---
- `:context`
	- `:hover`
		- when mouse moves
	- `:active`
		- active link
	- `first-letter`
		- operate on the first letter
	- `nth-child(2)`
		- the second child

Can be chained with other selectors

`span.x:hover { background-color:yellow }`
`.x:nth-child(even) { background-color:red }`
`<span class="x"> example </span>`
	
	The background is red, but turns yellow when the mouse touches it
---
## Positioning
(left, right, top, bottom)

`p.fixed { position: fixed; right:10%; top:20% }`
- stays on one spot in the browser fixed

`p.relative { position: relative; left:-10px }`
- relative to where it normally goes
`p.bigrelative { position: relative; left:-100px }`

`p.abs { position: absolute; left:10%; top:5% }`
- absolute positioning to the first parent that was positioned (often the page itself)

`p.zindex { z-index: 5; position: absolute; right: 11%; top:10% }`
- z-index can be used to order overlapping 

## Text Alignment
- margin
- text-align

`p.centered { margin-left: auto; margin-right: auto }`

```css
.flex { border: 1px solid blue; }
.flex-container { display: flex; align-items: center; justify-content: center; border: 1px solid red; width: 100%}
```
```html
<p class="flex"> not centered </p>
<p class="flex-container">
	<p class="flex"> centered </p>
	<p class="flex" style="width:5cm"> centered and narrow </p>
</p>
```

---
The space means ALL CHILDREN

`nav ul { list-style: none }`
- `ul` inside `nav` has no bullet points
	- `ul` are bullet list which has bullet points normally
`nav ul>li { display: inline-block }`
- list items inside `nav ul` are displayed without line breaks

For the first one, all `ul` inside `nav` are influenced, on the other hand, the second one only affects `li` ==directly== inside `ul`

---
The arrow means DIRECT CHILD

```css
em { font-style: italic }
p>em { font-style: bold}
```
all elements in `em` class are italics, it will also be bold if it is in a `<p>` tag

<em style="font-weight:bold"> em stands for emphasis </em>
<b style="font-style:italic"> b stands for bold </b>

---
The comma means OR

```css
h1, h2, h3, h4, h5 { text-decoration: underline }
h1, h2 { font-variant: small-caps }
```
Heading 1 to 5 are all underlined,
heading 1 and 2 are also in small caps. 

---
## File Upload
```html
<form action="http://buttercup.cs.ualberta.ca:9000/"
	enctype="multipart/form-data"
	method="get">
	Choose a file to upload <br>
	<input name="uploadFile" type="file"> <br>
	<input type="submit" value="Upload it">
</form>
```

<form action="http://buttercup.cs.ualberta.ca:9000/"
	enctype="multipart/form-data"
	method="get">
	Choose a file to upload <br>
	<input name="uploadFile" type="file"> <br>
	<input type="submit" value="Upload it">
</form>

## Size Units
- px
	- 1/96th of an inch
	- was the size of a pixel in 90s
- %
	- percentage of the containing element
- em
	- font size
		- 2em is twice the size of the font
- ex
	- height of the letter 'x' in the current font and font size
