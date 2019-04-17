# JQUERY

**With jQuery you select (query) HTML elements and perform "actions" on them**

*Basic Syntax*: `$(selector).action()`

* A `$` sign to define/access jQuery
* A `(selector)` to "query (or find)" HTML elements
* A jQuery `action()` to be performed on the element(s)

## The Document Ready Event

The function below guarantees that your HTML will be fully loaded before any script on jQuery file starts to run

```javascript
$(document).ready(function() {

  //jQuery methods go here...

});

// OR

$(function() {

});
```
## jQuery Selectors

jQuery selectors are used to "find" (or select) HTML elements based on their name, id, classes, types, attributes, values of attributes and much more.

All selectors in jQuery start with `$()`

* $("p") -> select all `<p>` elements on a page
* $("#test") -> select id `#test`
* $(".test") -> select class `.test`
* $(this) -> select the current HTML element
* $("p.intro") -> select all `<p>` elements with class `intro`
* $("p:first") -> select the first `<p>` element
* $("ul li:first") -> select the first `<li>` element of the first `<ul>`
* $("ul li:first-child") -> select the first `<li>` element of every `<ul>`
* $("[href]") -> select all elements with href attribute

## jQuery Event Methods

An event represents the precise moment when something happens

**Mouse Events**
* click
* dblclick
* mouseleave

**Keyboad Events**
* keypress
* keydown
* keyup

**Form Events**
* submit
* change
* focus
* blur

**Document/Window Events**
* load
* resize
* scroll
* undload

### The ON() Method

The `on()` method attaches one or more event handles for the selected elements.
Attach a click event to a `<p>` element:

```javascript
$("p").on("click", function(){
  $(this).hide();
});
```

or attach multiple event handlers to a `<p>` element:

```javascript
$("p").on({
  mouseenter: function(){
    $(this).css("background-color", "lightgray");
  },
  mouseleave: function(){
    $(this).css("background-color", "lightblue");
  },
  click: function(){
    $(this).css("background-color", "yellow");
  }
});
```

## Get Content

Three simple, but useful, jQuery methods for DOM manipulation are:

* `text()` - Set or Get the text content of selected elements
* `html()` - Set or Get the content of selected elements (ncluding HTML markup/tags)
* `val()` - Set or Get the value of form fields

```javascript
<script>
$(document).ready(function(){

  $("#btn1").click(function(){
    alert("Text: " + $("#test").text());
  });

  $("#btn2").click(function(){
    alert("HTML: " + $("#test").html());
  });

  $("#btn1").click(function(){
  alert("Value: " + $("#test").val());
  });

});
</script>
</head>
<body>

<p id="test">This is some <b>bold</b> text in a paragraph.</p>

<button id="btn1">Show Text</button>
<button id="btn2">Show HTML</button>
````

## Get Attributes

The jQuery `attr()` method is used to get attributes values.

```javascript
<script>
$(document).ready(function(){
  $("button").click(function(){
    alert($("#w3s").attr("href"));
  });
});
</script>
</head>
<body>

<p><a href="https://www.w3schools.com" id="w3s">W3Schools.com</a></p>

<button>Show href Value</button>
```

## Set Content and Attributes

You can use the same three methods from `Get Content` to **set content**

* `text()`
* `html()`
* `val()`

```javascript
$(document).ready(function(){
  $("#btn1").click(function(){
    $("#test1").text("Hello world!");
  });
  $("#btn2").click(function(){
    $("#test2").html("<b>Hello world!</b>");
  });
  $("#btn3").click(function(){
    $("#test3").val("Dolly Duck");
  });
});
</script>
</head>
<body>

<p id="test1">This is a paragraph.</p>
<p id="test2">This is another paragraph.</p>

<p>Input field: <input type="text" id="test3" value="Mickey Mouse"></p>

<button id="btn1">Set Text</button>
<button id="btn2">Set HTML</button>
<button id="btn3">Set Value</button>
```

**Set Attributes - attr()**

The following example demonstrates how to change (set) the value of the href attribute in a link:

```javascript
$("button").click(function(){
  $("#w3s").attr("href", "https://www.w3schools.com/jquery/");
});
```

The `attr()` mehtod also allows you to set mutiple attributes at the same time.

```javascript
$("button").click(function(){
  $("#w3s").attr({
    "href" : "https://www.w3schools.com/jquery/",
    "title" : "W3Schools jQuery Tutorial"
  });
});
```

## Add new HTML Content

jQuery have four method that are used to add new content

* `append()` - inserts content **AT THE END** of the selected elements
* `prepend()` - inserts content **AT THE BEGINNING** of the selected elements
* `after()` - inserts content **AFTER** the selected elements
* `before()` - inerts content **BEFORE** the selected elements

```javascript
// Append
$("p").append("Some appended text.");

function appendText() {
  var txt1 = "<p>Text.</p>";               // Create element with HTML
  var txt2 = $("<p></p>").text("Text.");   // Create with jQuery
  var txt3 = document.createElement("p");  // Create with DOM
  txt3.innerHTML = "Text.";
  $("body").append(txt1, txt2, txt3);      // Append the new elements
}

// Prepend
$("p").prepend("Some prepended text.");


// After and Before
$("img").after("Some text after");

$("img").before("Some text before");
```

## Remove Elements

To remove elements and content, there are mainly two jQuery methods:

* `remove()` - removes the selected elements (and its child elements)
* `empty()` - removes the child elements from the selected element

**Filter The Elements to be Removed**

The following example removes all `<p>` elements with `class=test`

```javascript
$("p").remove(".test");
````

## Get and Set CSS Classes

jQuery has several methods for CSS maipulation. We will look at the following methods:

* `addClass()` - adds one or more classes to the selected elements
* `removeClass()` - removes one or more classes from the selected elements
* `toggleClass()` - toggles between adding/removing classes from the selected elements
* `css()` - sets or returns the style attribute


### addClass()

```javascript
$("button").click(function(){
  $("h1, h2, p").addClass("blue");
  $("div").addClass("important");
});

// or even mutiple classes

$("button").click(function(){
  $("#div1").addClass("important blue");
});
```

### removeClass()

```javascript
$("button").click(function(){
  $("h1, h2, p").removeClass("blue");
});
```

### toggleClass()

```javascript
$("button").click(function(){
  $("h1, h2, p").toggleClass("blue");
});
```

### css()

The css() method sets or retuns one or more styles properties for the selected elements

```javascript
$("p").css("background-color", "yellow");

// or mutiple

$("p").css({"background-color": "yellow", "font-size": "200%"});

```
