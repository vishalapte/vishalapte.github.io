## Cover

### HTML

```html
<div id="cover" class="">
  <div id="cover-content" class="my-sm-auto">
    <div id="cover-container" class="container h-100">
      <div class="row h-100">
        <div class="col-12 col-sm-6">
          <div class="row align-items-stretch h-100 h-sm-unset">
            <div class="col-12">
              <img src="url_cover_text" 
                   class="text-center" 
                   width="100%" 
                   alt="Cover text">
            </div>
            <div class="col-12 align-self-middle align-self-sm-end"><div class="px-2">
              <a href="cta" class="btn btn-block py-2 text-white border-light">Convert Calls to Orders</a>
            </div></div>
          </div>
        </div>
        <div class="col-12 col-sm-6 align-self-middle">
          <img src="url_cover_image"
               class="text-center" 
               width="100%"
               alt="Cover image">
        </div>
      </div>
    </div>
  </div>
</div>
```

### CSS

```css
#cover {
  margin-top: -82px;
  padding-top: 82px;
  background-color: #180e29;
  height: 62.5vw;
  max-height: 675px;
  display: flex;
  justify-content: center;
}
#cover #cover-content {
  width: 100%;
}
#cover h1 {
  font-size: 2.5em;
  font-weight: 900;
  color: white;
}
@media screen and (max-width: 575px) and (orientation: portrait) {
  #cover {
    height: 100vh;
    max-height: 1024px;
  }
  #cover #cover-content {
    height: calc(100vh - 82px);
    max-height: 902px;
    width: calc(0.55 * (100vh - 124px));
    padding-bottom: 0;
  }
  #cover h1 {
    font-size: 2em;
  }
}
@media screen and (max-width: 767px) and (orientation: portrait) {
  #cover #cover-content {
    height: unset;
    max-height: unset;
  }
}
@media screen and (min-width: 576px) {
  .h-sm-unset { height: unset !important; }
}
@media screen and (min-width: 678px) {
  .h-md-unset { height: unset !important; }
}
@media screen and (min-width: 992px) {
  .h-lg-unset { height: unset !important; }
}
```
