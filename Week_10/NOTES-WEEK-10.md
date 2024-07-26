CSS

% = relative to parent
vh = relative to viewport/screen

The screen grows and shrink between these two:
min-width 
max-width

if you have
width: 25% = it will be 25% of the parent and it will shows only within the max width, 25% of the max width.

em = relative to parent
rem = 

breakpoint = styles breaks

Media Query
* media type: screen, print, speech, all
* media  feature: device-height, device=width, orientation, aspect ratio, light-level

```css
@media screen and (min-width: 250px) {
  h2 {
    color: purple;
  }
}
```

mobile phone
```css
@media screen and (orientation: landscape) {
  body {
    background color: yellow;
  }
}
```

mobile phone
```css
@media screen and (orientation: portrait) {
  body {
    background color: green;
  }
}
```

## CSS Preprocessor
* we are going to write CSS in a non-CSS language (Stylus, LESS, SASS)
* source code => preprocessor => finished file
.scss => node-sass => .css

### SASS 
sass-lang.com

* installation
```sass
npm install -g sass
```

* filename
```
filename.scss
```
* declare variable in sass by `$`
```
$fontColor: yellow;
```

* Example: (my-first-style.scss)
```my-first-style
h2 {
  font-size: 12 px;
  color: $fontColor;
}
```

* to run
```
sass my-first-style.scss output.css
```

* mixin
is a function

```css
@mixin createSquare($num, $color) {
  test-decoration: underline;
  border-radius: 15px;
  width: 2 * $num;
  height: $num;
  color: $(.)
}

```css
.square {
  @include createSquare();
  color: green;
}
```


<!-- index.html safe keeping -->
<article>
          <!-- Header: User info -->
          <header>
            <div>
              <i class="fa-regular fa-user"></i> &nbsp;
              John Doe
            </div>
            <div>
              @UserName
            </div>
          </header>
          <!-- User tweets -->
          <section>
            <p class="tweet-txt-container">Hello World!!!</p>
          </section>
          <!-- Footer: Time stamp and tweets icon -->
          <footer>
            <div>
              10 days
            </div>
            <div>
              <i class="fa-solid fa-flag"></i>&nbsp;
              <i class="fa-solid fa-retweet"></i>&nbsp;
              <i class="fa-solid fa-heart"></i>
            </div>
          </footer>
  
        </article>



