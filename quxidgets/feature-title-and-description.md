## Feature - Title &amp; Description

### JSON

```python
items = [
  {
    "icon": "<fontawesome icon>",
    "title": "<str:title>",
    "description": "<str:description>"
  },
  {
    "icon": "",
    "title": "",
    "description": ""
  }
]
```

### HTML

> This will achieve a 1 column display on mobile, 2 column display on small 
> devices upto but not including an iPad, and 3 column display on every 
> device starting with an iPad.

```html
<div>
  <div class="row">
    <div class="col-12 ">
      <div class="features-text section-header pl-3 text-left pl-md-0 text-md-center">
        <h2 class="section-title">Feature Section</h2>
      </div>
    </div>
  </div>

  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
  <!-- for item in items -->
    <div class="col mb-4"><div class="d-inline-flex">
      <div class="feature-icon align-self-start">
        <span class="fa-stack fa-2x">
          <i class="fas fa-circle fa-stack-2x"></i>
         <i class="item.icon fa-stack-1x fa-inverse"></i>
       </span>
      </div>
      <div class="feature-content align-self-start">
        <div class="font-weight-bold pb-2">
          item.title
        </div>
        <div>item.description</div>
      </div>
    </div></div>
  <!-- endfor -->
  </div>
</div>
```

### CSS

```css
.section-header {
  margin-top: 2.5rem;
  margin-bottom: 2.5rem;
}
.section-header h2 {
  font-size: 1.5rem;
  font-weight: 900;
  margin-bottom: 1.5rem;
}
.feature-icon {
  padding-left: 0;
  padding-right: 0.75rem;
}
```
