# Change Background

## Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/dR0veB0his4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Code

[Code](https://github.com/phptuts/chrome-extenison-10-minute)

## Icon Down

[Icons Zip](https://github.com/phptuts/changebackgroundchromeextension/raw/master/icons.zip)

## Manifest.json

```json
{
  "manifest_version": 3,
  "name": "Background Changer",
  "version": "1.0.0",
  "description": "Does stuff with the background.",
  "icons": {
    "128": "icon128.png",
    "48": "icon48.png",
    "16": "icon16.png"
  },
  "action": {
    "default_icon": "icon16.png",
    "default_popup": "popup.html"
  },
  "permissions": ["scripting", "tabs", "activeTab"]
}
```

## POPUP.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        width: 200px;
        height: 200px;
      }
      input {
        display: block;
        margin: 0 auto;
      }
      h2 {
        text-align: center;
      }
      #rotate,
      #rotate3d {
        width: 90%;
      }
    </style>
  </head>
  <body>
    <h2>Background Color</h2>
    <input type="color" id="color-changer" />
    <h2>Rotate Page</h2>
    <input type="range" min="0" max="360" step="1" value="0" id="rotate" />

    <h2>Rotate 3D</h2>
    <input type="range" min="0" max="360" step="1" value="0" id="rotate3d" />
    <script src="popup.js"></script>
  </body>
</html>
```

## POPUP.js

```js
const colorEl = document.getElementById("color-changer");

const rotateEl = document.getElementById("rotate");

const rotate3DEl = document.getElementById("rotate3d");

colorEl.addEventListener("input", () => {
  injectCSS(`body {
        background-color: ${colorEl.value}!important;
    }`);
});

rotateEl.addEventListener("input", () => {
  injectCSS(`body {
          transform: rotate(${rotateEl.value}deg)!important;
      }`);
});

rotate3DEl.addEventListener("input", () => {
  injectCSS(`body {
            transform: rotate3d(1,1,1,${rotate3DEl.value}deg)!important;
        }`);
});

function injectCSS(css) {
  chrome.tabs.query({ active: true, currentWindow: true }, ([tab]) => {
    if (!tab) return;
    chrome.scripting.insertCSS({
      css,
      target: { tabId: tab.id },
    });
  });
}
```
