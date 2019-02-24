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