## Christopher Duggan - Developer Quiz

#### 1) What is the difference between HTTP and HTTPS?

HyperText Transfer Protocol (HTTP) is the set of rules that define how information is passed from a web server to a browser. Information sent using HTTP travels as plain text, making it not very secure. HTTPS (the S stands for security) uses encryption when information is exchanged, which helps reduce security risk.

##### 2) What is the difference between HTTP GET and POST?

A GET request is sent asking that information be returned while a POST request sends information off. In very simple terms, GET is asking something and POST is telling something.

##### 3) What is the difference between the HTTP 2xx status codes and the 4xx status codes?

A 2xx response means that the HTTP request was successfully received. A 4xx response means there was some kind of error with the HTTP request on the client side.

##### 4) What is ajax (conceptually, what does it do)? Describe a situation where it is useful.

Ajax is way several different technologies can be combined to allow websites to be updated asynchronously, meaning one part of a page can be changed without needing to reload the entire page. Probably the most famous example of Ajax would be Google Suggest, the suggested responses that pop up after you type a bit in the search bar.

(looked up on https://en.wikipedia.org/wiki/Ajax_(programming) and https://www.w3schools.com/php/php_ajax_intro.asp)

##### 5) What is responsive design?

An approach to design that takes screens of different sizes into account and creates different ways of presenting a site to the user taking their screen size (and sometimes other factors) into account.

##### 6) What is the difference between these 3 CSS rules?

This rule applies to all div tags
```css
div {background:#fff;}
```
This rule applies to HTML tags that have "div" as their id (there should only be one)
```css
#div {background:#fff;}
```
This rule applies to HTML tags that have "div" as their class
```css
.div {background:#fff;}
```

##### 7) What is the difference between these 2 uses of the <script> tag?

```HTML
<script src="http://example.com/whatever.js"></script>
```
```HTML
<script>var whatever = true</script>
```
The first script tag references an external javascript file (whatever.js). The second is an "inline script," telling the browser to interpret "var whatever = true" as a script and not HTML.

##### 8) What is the difference between these two javascript snippets?

```javascript
var x = function() {
return 1+1;
}();
```

```javascript
var y = function() {
return 1+1;
};
```

The first snippet has a self-referential function call just before the final semicolon where the second doesn't. That means `x` will invoke the function and return `2` but to invoke the function associated with `y`, you'd have to use `y()`.

## Practical
---

##### 1. Write HTML/CSS to draw the following scene (inline css is fine if you want):
#####  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a. One red box, 200x200 pixels

#####  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;b. One blue box, 200x200 pixels

#####  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;c. One green box, 100x100 pixels

#####  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;d. The green box should be centered inside the red box

#####  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e. The red and blue boxes should not overlap

```HTML
<!DOCTYPE HTML>
<HTML>
  <head>
    <meta charset="UTF-8">
    <title>Boxes</title>
    <style>
      .box-200 { height: 200px; width: 200px;}
      .box-100 { height: 100px; width: 100px;}
      .red { background-color: red;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      .green { background-color: green;}
      .blue { background-color: blue;}
  </style>
  </head>
  <body>
    <div class="box-200 red">
    <div class="box-100 green"></div>
    </div>
    <div class="box-200 blue"></div>
  </body>
</HTML>
```

##### 2. You have started an analytics company with the domain "hashtag-analytics.com". You provide this tracking pixel for your customers to place on their websites. By summing the number of times the pixel was loaded, you calculate the number of visitors to each site.

```html
<img src="http://hashtag-analytics.com/12345/pixel.gif" width="1" height="1" />
```

##### As it stands, this pixel has a problem because it will be cached by the browser.

##### a. Why is caching a problem for the analytics company?

When the user visits a site, their browser will get the HTML page from the server, then check the cache to see if it contains our pixel image. If it does, it will load the image from the cache instead of loading it from the server.

##### b. How could you prevent browser caching? (use any technique(s) you want)

This subject is completely unfamiliar to me so forgive me if this isn't 100% technically accurate:
The browser can be "tricked" into thinking the image is a file different from the one in the cache by adding a unique parameter to the end of the image URL each time the site is loaded. A simple way to do this would be with by adding a timestamp to the image source with something like this in your javascript:

```javascript
const editSrc = () => {
let dateTime = new Date().getTime();
document.getElementById('pixel').src += '?' + dateTime;
};
```

Another method might be to add the header Cache-Control: no-store to the HTTP request for the image. I would have to do more research on how to properly do this before I could give a confident response about how it works exactly.

(Looked up several stack overflow questions as well as the MDN and W3 schools entries on Cache-Control)

##### c. What will happen if the customer's website is served over HTTPS? How could you modify the tracking pixel to fix that?

Instead of using `http://hashtag-analytics.etc...` for the image source, a protocol-relative URL could be used, ie. `//hashtag-analytics.etc...`

(looked up here https://support.google.com/tagmanager/forum/AAAAnP_FwdIgr8q46Fpy5c/?hl=en&gpf=d/topic/tag-manager/gr8q46Fpy5c and here https://www.paulirish.com/2010/the-protocol-relative-url/)

#### d. List some information the tracking company would collect (ex. IP address)

In addition to the IP address and the number of times a site is visited:

- Unique site views based on the IP address
- A general idea of a user's location
- The type of device and operating system the user is using
- Which pages the user visits on the site
- How long the user spends on each page
- Where the user clicks
- How they scroll
- Whether or not and for how long the user plays audio or video on the site

#### e. List some additional information (if any) that could be collected if a `<script>` tag is used instead of an `<img>` tag.

- User's searched keywords
- Browser plugins
- Screen resolution

(looked up here https://nativeads.com/blog/conversion-tracking-implementation/)

#### 3. Harder!
#### The following image tag appears somewhere on some webpage. The rest of the page is valid HTML, but otherwise unknown.

```html
<img id="myimage" src="http://hashtag-analytics.com/myimage.jpg" width="300" height="250"/>
```

#### Write CODE in plain javascript to do the following (jQuery is fine too, if you prefer):

#### Every 2 seconds:
#### &nbsp;&nbsp;&nbsp;- &nbsp;&nbsp;&nbsp;Check whether the image is viewable **
#### &nbsp;&nbsp;&nbsp;- &nbsp;&nbsp;&nbsp;If yes, write visible to the console (that is, window.console)
#### &nbsp;&nbsp;&nbsp;- &nbsp;&nbsp;&nbsp;If no, do nothing

#### ** the image is viewable if any part of it appears on the screen (so if the image is entirely above or below the viewport, then the user cannot see it, so it is not considered "viewable"). You can ignore horizontal bounds checking.

```javascript
const isVisible = () => {
  let img = document.getElementById('myimage');
  let top = img.getBoundingClientRect().top;
  let bottom = img.getBoundingClientRect().bottom;

  if (
    bottom >= 0 &&
    top <= (window.innerHeight && document.documentElement.clientHeight)
  ) {
    console.log('visible');
  }
  setTimeout(isVisible, 2000);
};

isVisible();
```

(modified this code https://gomakethings.com/how-to-test-if-an-element-is-in-the-viewport-with-vanilla-javascript/)
