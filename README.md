## 1. Asynchronous Stylesheet Loading
```
<link 
  rel="stylesheet" 
  href="https://googleapis.com" 
  media="print" 
  onload="this.media='all'; this.onload=null;"
>
```

## 2. Using font-display (Standard CSS Method)
```
@font-face {
  font-family: 'MyCustomFont';
  src: url('myfont.woff2') format('woff2');
  font-display: swap; /* Defer-like behavior: shows text immediately */
}
```

## 3. CSS Font Loading API (JavaScript Control)
```
// javascript
const myFont = new FontFace('MyFont', 'url(myfont.woff2)');

myFont.load().then(function(loadedFont) {
  document.fonts.add(loadedFont);
  document.body.style.fontFamily = 'MyFont, sans-serif';
}).catch(function(error) {
  console.error('Font loading failed:', error);
});
```

## 4. Optimize with Preconnect
```
html<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

## Summary Comparison

| Method                     | Impact            | Best For |
|-----------------------------------------------------------|
| font-display: swap | Immediate text visibility | General use; prevents "invisible" text. |
|-----------------------------------------------------------|
| Media Hack         | Non-blocking 			 | External swap stylesheets (Google Fonts). |
|-----------------------------------------------------------|
| Font Loading API	 | Full programmatic control | Interactive apps or complex lazy-loading. |


