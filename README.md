```
@font-face {
  font-family: "bahnschrift";
  src:
    url("bahnschrift-webfont.woff2") format("woff2"),
    url("bahnschrift-webfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}
```
Let's go through it to see what it does:

  - **font-family**: This line specifies the name you want to refer to the font as. This can be anything you 
    like as long as you use it consistently throughout your CSS.
  - **src**: These lines specify the paths to the font files to be imported into your CSS (the url part), and 
    the format of each font file (the format part). The latter part in each case is optional, but it is useful 
    to declare because it allows browsers to determine which font they can use more quickly. Multiple 
    declarations can be listed, separated by commas. Because the browser will search through them according 
    to the rules of the cascade, it's best to state your preferred formats, like WOFF2, at the beginning.
  - **font-weight/font-style**: These lines specify what weight the font has and whether it is italic or not. 
    If you are importing multiple weights of the same font, you can specify what their weight/style is 
	and then use different values of font-weight/font-style to choose between them, rather than having 
	to give all the members of the font family different names. @font-face tip: define font-weight and 
	font-style to keep your CSS simple by Roger Johansson shows what to do in more detail.
  - **font-display**: This line specifies how the font is displayed while it is loading.
  

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
| -------------------------- | ------------------------------- | ---- |
| font-display: swap | Immediate text visibility | General use; prevents "invisible" text. |
| Media Hack         | Non-blocking 			 | External swap stylesheets (Google Fonts). |
| Font Loading API	 | Full programmatic control | Interactive apps or complex lazy-loading. |


