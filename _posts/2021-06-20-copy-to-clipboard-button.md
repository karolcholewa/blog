---
layout: post
title: "Copy to Clipboard Button"
categories: [Web]
---

This is a small but significant enhancement to my blog posts. I've added a button to copy code to the clipboard. This was missing from the default setup of the Jekyll.

## Script for Adding a Button to All Posts
This snippet creates a button inside the code block and uses the Navigator.Clipboard API to copy contents of the code block. I've created a new file at assets\post.js and referenced it in the bottom of the _layouts\post.html like so: 

```javascript
<script src="{{ site.baseurl }}/assets/post.js"></script>
```

```javascript
var codeBlocks = document.querySelectorAll('pre.highlight');

codeBlocks.forEach(function (codeBlock) {
  var copyButton = document.createElement('button');
  copyButton.className = 'copy';
  copyButton.type = 'button';
  copyButton.ariaLabel = 'Copy code to clipboard';
  copyButton.innerText = 'Copy';

  codeBlock.append(copyButton);

  copyButton.addEventListener('click', function () {
    var code = codeBlock.querySelector('code').innerText.trim();
    window.navigator.clipboard.writeText(code);

    copyButton.innerText = 'Copied';
    var fourSeconds = 4000;

    setTimeout(function () {
      copyButton.innerText = 'Copy';
    }, fourSeconds);
  });
});
```
## CSS
To change the default appearance I've updated the assets\style.scss to match the code highlighter style.

```css
pre.highlight > button {
    background: #282a36;
    padding: 0.5em;
    min-width: 5em;
    border: 1px solid #f8f8f2;
    color: #f8f8f2;
    margin-top: 1em;
}
```

## Credit
I found the matching solution for Jekyll on the following blog: https://remarkablemark.org/blog/. Credit goes to RemarkableMark.

## Resources:

*   [Jekyll: Copy code to clipboard](https://remarkablemark.org/blog/2021/06/01/add-copy-code-to-clipboard-button-to-jeyll-site/)