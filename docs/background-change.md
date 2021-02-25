# Change Background

## Video

## Code

[Code](https://github.com/phptuts/changebackgroundchromeextension)

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
  "permissions": ["activeTab"]
}
```

## POPUP.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
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

colorEl.addEventListener("input", (e) => {
  const hexValue = e.target.value;
  chrome.tabs.executeScript(null, {
    code: `document.body.style.backgroundColor='${hexValue}'`,
  });
});

rotateEl.addEventListener("input", (e) => {
  const degree = e.target.value;
  chrome.tabs.executeScript(null, {
    code: `document.body.style.transform='rotate(${degree}deg)'`,
  });
});

rotate3DEl.addEventListener("input", (e) => {
  const degree = e.target.value;
  chrome.tabs.executeScript(null, {
    code: `document.body.style.transform='rotate3d(1, 1, 1,${degree}deg)'`,
  });
});
```
