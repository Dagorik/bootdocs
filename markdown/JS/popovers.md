@page javascript-popovers PopOvers
@parent javascript 8

Add small overlays of content, like those on the iPad, to any element for housing secondary information.

Popovers whose both title and content are zero-length are never displayed.

### Plugin dependency
Popovers require the [tooltip plugin](/javascript-tooltips.html#section_Statictooltip) to be included in your version of Bootstrap.

### Opt-in functionality
For performance reasons, the Tooltip and Popover data-apis are opt-in, meaning you must initialize them yourself.

One way to initialize all popovers on a page would be to select them by their `data-toggle` attribute:

```
$(function () {
  $('[data-toggle="popover"]').popover()
})
```

### Popovers in button groups and input groups require special setting
When using popovers on elements within a `.btn-group` or an `.input-group`, you'll have to specify the option `container: 'body'` (documented below) to avoid unwanted side effects (such as the element growing wider and/or losing its rounded corners when the popover is triggered).

### Don't try to show popovers on hidden elements
Invoking `$(...).popover('show')` when the target element is `display: none;` will cause the popover to be incorrectly positioned.

### Popovers on disabled elements require wrapper elements
To add a popover to a `disabled` or `.disabled` element, put the element inside of a `<div>` and apply the popover to that `<div>` instead.

### Multiple-line links
Sometimes you want to add a popover to a hyperlink that wraps multiple lines. The default behavior of the popover plugin is to center it horizontally and vertically. Add `white-space: nowrap;` to your anchors to avoid this.





## Examples

### Static Popover
Four options are available: top, right, bottom, and left aligned.

@demo demos/js-popovers-static/demo.html

### Live Demo

@demo demos/js-popovers-live/demo.html

### Four Directions

@demo demos/js-popovers-directions/demo.html


### Dismiss on next click
Use the `focus trigger` to dismiss popovers on the next click that the user makes.

### Specific markup required for dismiss-on-next-click
For proper cross-browser and cross-platform behavior, you must use the `<a>` tag, not the `<button>` tag, and you also must include the `role="button"` and `tabindex` attributes.

@demo demos/js-popovers-dismiss/demo.html

## Usage
Enable popovers via JavaScript:

```
$('#example').popover(options)
```

## Options
Options can be passed via data attributes or JavaScript. For data attributes, append the option name to `data-`, as in `data-animation=""`.

<table class="table table-bordered table-striped js-options-table js-options-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Type</th>
          <th>Default</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>animation</td>
          <td>boolean</td>
          <td>true</td>
          <td>Apply a CSS fade transition to the popover</td>
        </tr>
        <tr>
          <td>container</td>
          <td>string | false</td>
          <td>false</td>
          <td>
            <p>Appends the popover to a specific element. Example: <code>container: 'body'</code>. This option is particularly useful in that it allows you to position the popover in the flow of the document near the triggering element -&nbsp;which will prevent the popover from floating away from the triggering element during a window resize.</p>
          </td>
        </tr>
        <tr>
          <td>content</td>
          <td>string | function</td>
          <td>''</td>
          <td>
            <p>Default content value if <code>data-content</code> attribute isn't present.</p>
            <p>If a function is given, it will be called with its <code>this</code> reference set to the element that the popover is attached to.</p>
          </td>
        </tr>
        <tr>
          <td>delay</td>
          <td>number | object</td>
          <td>0</td>
          <td>
           <p>Delay showing and hiding the popover (ms) - does not apply to manual trigger type</p>
           <p>If a number is supplied, delay is applied to both hide/show</p>
           <p>Object structure is: <code>delay: { "show": 500, "hide": 100 }</code></p>
          </td>
        </tr>
        <tr>
          <td>html</td>
          <td>boolean</td>
          <td>false</td>
          <td>Insert HTML into the popover. If false, jQuery's <code>text</code> method will be used to insert content into the DOM. Use text if you're worried about XSS attacks.</td>
        </tr>
        <tr>
          <td>placement</td>
          <td>string | function</td>
          <td>'right'</td>
          <td>
            <p>How to position the popover - top | bottom | left | right | auto.<br>When "auto" is specified, it will dynamically reorient the popover. For example, if placement is "auto left", the popover will display to the left when possible, otherwise it will display right.</p>
            <p>When a function is used to determine the placement, it is called with the popover DOM node as its first argument and the triggering element DOM node as its second. The <code>this</code> context is set to the popover instance.</p>
          </td>
        </tr>
        <tr>
          <td>selector</td>
          <td>string</td>
          <td>false</td>
          <td>If a selector is provided, popover objects will be delegated to the specified targets. In practice, this is used to enable dynamic HTML content to have popovers added. See <a href="https://github.com/twbs/bootstrap/issues/4215">this</a> and <a href="http://jsbin.com/zopod/1/edit">an informative example</a>.</td>
        </tr>
        <tr>
          <td>template</td>
          <td>string</td>
          <td><code>'&lt;div class="popover" role="tooltip"&gt;&lt;div class="arrow"&gt;&lt;/div&gt;&lt;h3 class="popover-title"&gt;&lt;/h3&gt;&lt;div class="popover-content"&gt;&lt;/div&gt;&lt;/div&gt;'</code></td>
          <td>
            <p>Base HTML to use when creating the popover.</p>
            <p>The popover's <code>title</code> will be injected into the <code>.popover-title</code>.</p>
            <p>The popover's <code>content</code> will be injected into the <code>.popover-content</code>.</p>
            <p><code>.arrow</code> will become the popover's arrow.</p>
            <p>The outermost wrapper element should have the <code>.popover</code> class.</p>
          </td>
        </tr>
        <tr>
          <td>title</td>
          <td>string | function</td>
          <td>''</td>
          <td>
            <p>Default title value if <code>title</code> attribute isn't present.</p>
            <p>If a function is given, it will be called with its <code>this</code> reference set to the element that the popover is attached to.</p>
          </td>
        </tr>
        <tr>
          <td>trigger</td>
          <td>string</td>
          <td>'click'</td>
          <td>How popover is triggered - click | hover | focus | manual. You may pass multiple triggers; separate them with a space. <code>manual</code> cannot be combined with any other trigger.</td>
        </tr>
        <tr>
          <td>viewport</td>
          <td>string | object | function</td>
          <td>{ selector: 'body', padding: 0 }</td>
          <td>
            <p>Keeps the popover within the bounds of this element. Example: <code>viewport: '#viewport'</code> or <code>{ "selector": "#viewport", "padding": 0 }</code></p>
            <p>If a function is given, it is called with the triggering element DOM node as its only argument. The <code>this</code> context is set to the popover instance.</p>
          </td>
       </tr>
      </tbody>
    </table>

### Data attributes for individual popovers
Options for individual popovers can alternatively be specified through the use of data attributes, as explained above.

## Methods
`$().popover(options)`
Initializes popovers for an element collection.

`.popover('show')`
Reveals an element's popover. Returns to the caller before the popover has actually been shown (i.e. before the `shown.bs.popover` event occurs). This is considered a "manual" triggering of the popover. Popovers whose both title and content are zero-length are never displayed.

```
$('#element').popover('show')
```

`.popover('hide')`
Hides an element's popover. Returns to the caller before the popover has actually been hidden (i.e. before the `hidden.bs.popover` event occurs). This is considered a "manual" triggering of the popover.

```
$('#element').popover('hide')
```

`.popover('toggle')`
Toggles an element's popover. Returns to the caller before the popover has actually been shown or hidden (i.e. before the `shown.bs.popover` or `hidden.bs.popover` event occurs). This is considered a "manual" triggering of the popover.

```
$('#element').popover('toggle')
```

`.popover('destroy')`
Hides and destroys an element's popover. Popovers that use delegation (which are created using the selector option) cannot be individually destroyed on descendant trigger elements.

```
$('#element').popover('destroy')
```

## Events
<table class="table table-bordered table-striped bs-events-table">
      <thead>
        <tr>
          <th>Event Type</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>show.bs.popover</td>
          <td>This event fires immediately when the <code>show</code> instance method is called.</td>
        </tr>
        <tr>
          <td>shown.bs.popover</td>
          <td>This event is fired when the popover has been made visible to the user (will wait for CSS transitions to complete).</td>
        </tr>
        <tr>
          <td>hide.bs.popover</td>
          <td>This event is fired immediately when the <code>hide</code> instance method has been called.</td>
        </tr>
        <tr>
          <td>hidden.bs.popover</td>
          <td>This event is fired when the popover has finished being hidden from the user (will wait for CSS transitions to complete).</td>
        </tr>
        <tr>
          <td>inserted.bs.popover</td>
          <td>This event is fired after the <code>show.bs.popover</code> event when the popover template has been added to the DOM.</td>
        </tr>
      </tbody>
    </table>
