## Pricing

```html
<div class="row pricing-tables">
  <div class="col-12 col-lg-4 mb-4 d-flex">
    <div class="shark-card">
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
            <div class="col-12 align-self-end pricing-features shark-card-body">
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
