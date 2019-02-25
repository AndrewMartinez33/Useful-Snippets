# Useful-Snippets

Feel free to use these snippets for whatever you want.

## Zoom When In View

---

An element is initially hidden on the page. When it is in the viewport, the element will become visible and zoom to 100%. When the element is out of the viewport it will become hidden again. Just add the 'hidden' class to any element. 

JavaScript

```js
window.addEventListener('scroll', zoomWhenInView);

function zoomWhenInView() {
  const elements = document.querySelectorAll('.hidden');
  elements.forEach(element => {
    // return object with the height and width of the element, along with its distance from the top, bottom, right, and left.
    const distances = element.getBoundingClientRect();
    // if the element exits the viewport from the top completely
    if (distances.top <= (- distances.height)) {
      if (element.classList.contains('zoom')) {
        element.classList.remove('zoom');
      }
    }

    // if the element exits the viewport from the bottom completely
    if (distances.top > ((window.innerHeight || document.documentElement.clientHeight))) {
      if (element.classList.contains('zoom')) {
        element.classList.remove('zoom');
      }
    }

    //if the element is within the boundaries of the viewport
    if (distances.top >= 0 &&
      distances.left >= 0 &&
      distances.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
      distances.right <= (window.innerWidth || document.documentElement.clientWidth)) {
      element.classList.add('zoom');
    }
  })
}
```

CSS

```CSS
.hidden {
  visibility: hidden;
  transform: scale(.5);
}

.zoom {
  visibility: visible;
  transform: scale(1);
  transition: transform 1.2s;
}
```
HTML

```HTML
<div class="hidden">
  put something here
</div>
```

## Lazy Image Loader

---

Lazy loads images on scroll event if the image element is in the viewport.

JavaScript

```js
window.addEventListener('scroll', lazyLoader);


function lazyLoader() {
  const elements = document.querySelectorAll('.lazy-load');
  elements.forEach(element => {
    // return object with the height and width of the element, along with its distance from the top, bottom, right, and left.
    const distances = element.getBoundingClientRect();

    //if the element is within the boundaries of the viewport
    if (distances.top >= 0 &&
      distances.left >= 0 &&
      distances.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
      distances.right <= (window.innerWidth || document.documentElement.clientWidth)) {

      const imageSource = element.getAttribute('data-src');
      element.setAttribute('src', imageSource);
    }
  })
}
```

HTML

```HTML
<img class="lazy-load" src="initial image url" data-src="new image url" alt="blah blah blah">
```

## CSS Starter
---

This is my CSS starter sheet. Includes CSS reset, and some CSS variables with some of my preferred setting.

```CSS
/* CSS VARIABLES */

:root {
  --header-color-bg: #42a5f5;
  --footer-color-bg: #263238;
  --headline-font: Arial, Helvetica, sans-serif;
  --paragraph-font: Georgia, 'Times New Roman', Times, serif;
  --shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
  --shadow-lg: 0 1rem 3rem rgba(0, 0, 0, 0.175);
  --danger: #ff4444;
  --danger-dark: #CC0000;
  --warning: #ffbb33;
  --warning-dark: #FF8800;
  --success: #00C851;
  --success-dark: #007E33;
  --info: #33b5e5;
  --info-dark: #0099CC;
}

/* CSS RESET */

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

/* HTML5 display-role reset for older browsers */

article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}

body {
  line-height: 1;
}

ol,
ul {
  list-style: none;
}

blockquote,
q {
  quotes: none;
}

blockquote:before,
blockquote:after,
q:before,
q:after {
  content: '';
  content: none;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

a:link,
a:visited,
a:hover,
a:active {
  text-decoration: none;
}

body {
  overflow-x: hidden;
}


/* FLEXBOX STICKY FOOTER */
/* Simplest way I know of to keep footer at bottom of page */
/* 
  <body class="Site">
    <header>…</header>
    <main class="Site-content">…</main>
    <footer>…</footer>
  </body> 
*/

.Site {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}

.Site-content {
  flex: 1;
}


/* MEDIA QUERIES */

/* Extra small */

@media (min-width: 400px) {}

/* Small devices */

@media (min-width: 576px) {}

/* Medium devices */

@media (min-width: 768px) {}

/* Large devices */

@media (min-width: 992px) {}

/* Extra large */

@media (min-width: 1200px) {}

/* Super large */

@media (min-width: 1500px) {}
}