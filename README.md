# getting-started-custom-elements
create native custom elements with vanilla javascript - step by step example

## Steps

* Create html
```html
  <!doctype html>
  <html>
    <head>
      <base href="/">
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
      <title>Getting Started with Custom Elements</title>
    </head>
    <body>
      <star-rating></star-rating>
      <script>
        /// add your javascript here
      </script>
    </body>
  </html>
```

* Defining an element

  ```javascript
  class StartRatingElement extends HTMLElement {

    constructor() {
      super();
    }

  }

  // * Rules on creating custom elements
  //  * The name of a custom element must contain a dash (-). 
  //     This requirement is so the HTML parser can distinguish 
  //     custom elements from regular elements.
  //  * You can't register the same tag more than once.
  //  * Always write a closing tag (<star-rating></star-rating>).
  customElements.define('star-rating', StartRatingElement);
  ```

* Adding Properties and Attibutes 

  ```javascript
  class StartRatingElement extends HTMLElement {

    constructor() {
      super();
    }

    /// list of attribute expose to the browser
    /// ie. <star-rating checked></star-rating>
    static get observedAttributes() {
      return [ 'checked' ];
    }

    /// called when attribute change from the dom
    /// check if custom element has checked attribute
    /// i.e <star-rating checked></star-rating>
    ///   since <star-rating> element has attribute it will return true;
    get checked() {
      return this.hasAttribute('checked');
    }

    /// call when attribute change from the dom
    set checked(value) {
      /// find the span element then add or remove a class to span
      /// if the value === true, it will add 'checked' class to the span element
      ///   i.e <span class="checked"></span>
      const span = this.querySelector('span');
      if (value) {
        span.classList.add('checked');
      } else {
        span.classList.remove('checked');
      }
    }

    /// called when an observed attribute has been added, removed, updated, or replaced. 
    //  Note: only attributes listed in the observedAttributes property will receive this callback.
    attributeChangedCallback(name, oldValue, newValue) {
      switch(name) {
        case 'checked':
          this.checked = this.checked;
          break;
      }
    }

  }
  ```

* Add markup and style

```javascript
  class StartRatingElement extends HTMLElement {

    constructor() {
      super();
    }

    /// list of attribute expose to the browser
    /// ie. <star-rating checked></star-rating>
    static get observedAttributes() {
      return [ 'checked' ];
    }

    /// call or execute of attribute change from the dom
    /// check if custom element has checked attribute
    /// i.e <star-rating checked></star-rating>
    ///   since <star-rating> element has attribute it will return true;
    get checked() {
      return this.hasAttribute('checked');
    }

    /// call or execute of attribute change from the dom
    set checked(value) {
      /// find the span element then add or remove a class to span
      /// if the value = true, it will add 'checked' class to the span element
      ///   i.e <span class="checked"></span>
      const span = this.querySelector('span');
      if (value) {
        span.classList.add('checked');
      } else {
        span.classList.remove('checked');
      }
    }

    /// called when an observed attribute has been added, removed, updated, or replaced. 
    //  Note: only attributes listed in the observedAttributes property will receive this callback.
    attributeChangedCallback(name, oldValue, newValue) {
      switch(name) {
        case 'checked':
          this.checked = this.checked;
          break;
      }
    }

    /// called every time the element is inserted into the DOM. 
    /// useful for running setup code, such as fetching resources or rendering.
    connectedCallback() {
      const template = document.createElement('template');
      template.innerHTML = `
        <style>
          .checked svg {
            fill: orange;
          }
          span svg {
            width: 2%;
          }
        </style>
        <span>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
            <path d="M259.3 17.8L194 150.2 47.9 171.5c-26.2 3.8-36.7 36.1-17.7 54.6l105.7 103-25 145.5c-4.5 26.3 23.2 46 46.4 33.7L288 439.6l130.7 68.7c23.2 12.2 50.9-7.4 46.4-33.7l-25-145.5 105.7-103c19-18.5 8.5-50.8-17.7-54.6L382 150.2 316.7 17.8c-11.7-23.6-45.6-23.9-57.4 0z"/>
          </svg>
        </span>
      `;
      /// this will add the element to the dom
      this.appendChild(template.content);
    }
  }
```

* Adding event 

```javascript
  class StartRatingElement extends HTMLElement {

    constructor() {
      super();
    }

    /// list of attribute expose to the browser
    /// ie. <star-rating checked></star-rating>
    static get observedAttributes() {
      return [ 'checked' ];
    }

    /// call or execute of attribute change from the dom
    /// check if custom element has checked attribute
    /// i.e <star-rating checked></star-rating>
    ///   since <star-rating> element has attribute it will return true;
    get checked() {
      return this.hasAttribute('checked');
    }

    /// call or execute of attribute change from the dom
    set checked(value) {
      /// find the span element then add or remove a class to span
      /// if the value = true, it will add 'checked' class to the span element
      ///   i.e <span class="checked"></span>
      const span = this.querySelector('span');
      if (value) {
        span.classList.add('checked');
      } else {
        span.classList.remove('checked');
      }
    }

    /// called when an observed attribute has been added, removed, updated, or replaced. 
    //  Note: only attributes listed in the observedAttributes property will receive this callback.
    attributeChangedCallback(name, oldValue, newValue) {
      switch(name) {
        case 'checked':
          this.checked = this.checked;
          break;
      }
    }

    /// called every time the element is inserted into the DOM. 
    /// useful for running setup code, such as fetching resources or rendering.
    connectedCallback() {
      const template = document.createElement('template');
      template.innerHTML = `
        <style>
          .checked svg {
            fill: orange;
          }
          span svg {
            width: 2%;
          }
        </style>
        <span>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
            <path d="M259.3 17.8L194 150.2 47.9 171.5c-26.2 3.8-36.7 36.1-17.7 54.6l105.7 103-25 145.5c-4.5 26.3 23.2 46 46.4 33.7L288 439.6l130.7 68.7c23.2 12.2 50.9-7.4 46.4-33.7l-25-145.5 105.7-103c19-18.5 8.5-50.8-17.7-54.6L382 150.2 316.7 17.8c-11.7-23.6-45.6-23.9-57.4 0z"/>
          </svg>
        </span>
      `;
      /// this will add the element to the dom
      this.appendChild(template.content);

      /// add click event to the element
      this.addEventListener('click', function(e) {
        if (this.checked) {
          this.removeAttribute('checked');
        } else {
          this.setAttribute('checked', '')
        }
      })
    }

  }
```
