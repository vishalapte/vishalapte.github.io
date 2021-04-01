## Pricing

### HTML

```html
<div class="row pricing-tables">
  <div class="col-12 col-lg-4 mb-4 d-flex">
    <div class="quxidget-card shadow">
      <div class="row">
        <div class="col-12 col-sm-6 col-lg-12">
          <div class="row px-2">
            <div class="col-12"></div>
            <div class="col-12 align-self-start">
              <div class="pricing-header font-weight-bold">plan.name</div>
            </div>
            <div class="col-12 align-self-end py-2">
              <div class="pricing-price">
                <span class="price">plan.price</span> per plan.unit
              </div>
            </div>
            <div class="col-12 align-self-start pb-2">
              <div class="pricing-description">plan.description</div>
            </div>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-lg-12">
          <div class="row px-2">
            <div class="col-12 align-self-end pricing-features">
              <p>Includes:</p>
              <ul class="fa-ul">
                {% for feature in plan.features %}
                <li><span class="fa-li"><i class="fab fa-check"></i></span> feature</li>
                {% endfor %}
              </ul>
            </div>
            <div class="col-12 align-self-end pt-2">
              <div class="pricing-cta">
                <a href="plan.cta" class="btn btn-block py-2 btn-dark text-white">Purchase</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

### CSS

> Included in quxidget.css

```css
.quxidget-card {
  padding: 1.25rem 1rem;
  border: rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  width: 100%;
}
```    

### Javascript

> Included in quxidget.js

```javascript
function maxSelectorHeight(selector) {
    return Math.max.apply(null, $(selector).map(function () {
        return $(this).height();
    }).get());
}

function equalizeSelectorHeights(selector) {
    let maxHeight = maxSelectorHeight(selector);
    $(selector).each(function () {
        $(this).css('height', maxHeight + "px");
    });
}
```

```javascript
function sizePricingCards() {
  let width = $(window).width();
  if ($(window).width() > 991) {
    equalizeSelectorHeights('.pricing-description');
    equalizeSelectorHeights('.pricing-features');
  }
}

$(document).ready(function() {
  sizePricingCards();
  $(window).resize(function() {
    sizePricingCards();
  });
});
```
