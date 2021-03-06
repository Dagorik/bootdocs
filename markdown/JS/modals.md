@page javascript-modals Modals
@parent javascript 2

Modals are streamlined, but flexible, dialog prompts with the minimum required functionality and smart defaults.

> ### Multiple open modals not supported
> Be sure not to open a modal while another is still visible. Showing more than one modal at a time requires custom code.

> ### Modal markup placement
> Always try to place a modal's HTML code in a top-level position in your document to avoid other components affecting the > modal's appearance and/or functionality.

> ### Mobile device caveats
> There are some caveats regarding using modals on mobile devices. [See our browser support docs](http://getbootstrap.com/getting-started/#support-fixed-position-keyboards) for details.

**Due to how HTML5 defines its semantics, the `autofocus` HTML attribute has no effect in Bootstrap modals.** To achieve the same effect, use some custom JavaScript:

```
$('#myModal').on('shown.bs.modal', function () {
  $('#myInput').focus()
})

```

## Examples

### Static example
A rendered modal with header, body, and set of actions in the footer.

@demo demos/js-modals/demo.html 


## Live demo
Toggle a modal via JavaScript by clicking the button below. 

@demo demos/js-modals/live-example/demo.html

> ### Make modals accessible
> Be sure to add `role="dialog"` and `aria-labelledby="..."`, referencing the modal title, to `.modal`, and `role="document">` to the `.modal-dialog` itself.
>
> Additionally, you may give a description of your modal dialog with `aria-describedby` on `.modal`.

> ###Embedding YouTube videos
> Embedding YouTube videos in modals requires additional JavaScript not in Bootstrap to automatically stop playback and more> . [See this helpful Stack Overflow post](https://stackoverflow.com/questions/18622508/bootstrap-3-and-youtube-in-modal) for more information.

## Optional sizes
Modals have two optional sizes, available via modifier classes to be placed on a `modal-dialog`.

@demo demos/js-modals/optional-sizes/demo.html 

## Remove animation
For modals that simply appear rather than fade in to view, remove the .fade class from your modal markup.

```
<div class="modal" tabindex="-1" role="dialog" aria-labelledby="...">
  ...
</div>
```

## Using the grid system
To take advantage of the Bootstrap grid system within a modal, just nest `.container-fluid` within the `.modal-body` and then use the normal grid system classes within this container.

@demo demos/js-modals/using-grid-system/demo.html 

## Varying modal content based on trigger button
Have a bunch of buttons that all trigger the same modal, just with slightly different contents? Use `event.relatedTarget` and [HTML `data-*` attributes](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes) (possibly via [jQuery](http://api.jquery.com/data/)) to vary the contents of the modal depending on which button was clicked. See the Modal Events docs for details on `relatedTarget`.

@demo demos/js-modals/varying-modal/demo.html 

## Options
Options can be passed via data attributes or JavaScript. For data attributes, append the option name to `data-`, as in `data-offset=""`.

```
$('#exampleModal').on('show.bs.modal', function (event) {
  var button = $(event.relatedTarget) // Button that triggered the modal
  var recipient = button.data('whatever') // Extract info from data-* attributes
  // If necessary, you could initiate an AJAX request here (and then do the updating in a callback).
  // Update the modal's content. We'll use jQuery here, but you could use a data binding library or other methods instead.
  var modal = $(this)
  modal.find('.modal-title').text('New message to ' + recipient)
  modal.find('.modal-body input').val(recipient)
})
```

## Usage
The modal plugin toggles your hidden content on demand, via data attributes or JavaScript. It also adds `.modal-open` to the `<body>` to override default scrolling behavior and generates a .modal-backdrop to provide a click area for dismissing shown modals when clicking outside the modal.

### Via data attributes
Activate a modal without writing JavaScript. Set `data-toggle="modal"` on a controller element, like a button, along with a `data-target="#foo"` or `href="#foo"` to target a specific modal to toggle.

```
<button type="button" data-toggle="modal" data-target="#myModal">Launch modal</button>
```

### Via JavaScript
Call a modal with id myModal with a single line of JavaScript:

```
$('#myModal').modal(options)
```
## Options
Options can be passed via data attributes or JavaScript. For data attributes, append the option name to `data-`, as in `data-backdrop=""`.

<table class="table table-bordered table-striped js-options-table">
  <thead>
   <tr>
     <th>Name</th>
     <th>type</th>
     <th>default</th>
     <th>description</th>
   </tr>
  </thead>
  <tbody>
   <tr>
     <td>backdrop</td>
     <td>boolean or the string <code>'static'</code></td>
     <td>true</td>
     <td>Includes a modal-backdrop element. Alternatively, specify <code>static</code> for a backdrop which doesn't close the modal on click.</td>
   </tr>
   <tr>
     <td>keyboard</td>
     <td>boolean</td>
     <td>true</td>
     <td>Closes the modal when escape key is pressed</td>
   </tr>
   <tr>
     <td>show</td>
     <td>boolean</td>
     <td>true</td>
     <td>Shows the modal when initialized.</td>
   </tr>
   <tr>
     <td>remote</td>
     <td>path</td>
     <td>false</td>
     <td>
      <p><strong class="text-danger">This option is deprecated since v3.3.0 and will be removed in v4.</strong> We recommend instead using client-side templating or a data binding framework, or calling <a href="http://api.jquery.com/load/">jQuery.load</a> yourself.</p>
      <p>If a remote URL is provided, <strong>content will be loaded one time</strong> via jQuery's <code>load</code> method and injected into the <code>.modal-content</code> div. If you're using the data-api, you may alternatively use the <code>href</code> attribute to specify the remote source. An example of this is shown below:</p>
      <pre><code>&lt;a data-toggle="modal" href="remote.html" data-target="#modal"&gt;Click me&lt;/a&gt;</code></pre>
     </td>
   </tr>
  </tbody>
</table>

## Methods
### *.modal(options)*

Activates your content as a modal. Accepts an optional options `object`.

```
$('#myModal').modal({
  keyboard: false
})
```


### *.modal('toggle')*
Manually toggles a modal. **Returns to the caller before the modal has actually been shown or hidden** (i.e. before the shown `.bs.modal` or `hidden.bs.modal` event occurs).
```
$('#myModal').modal('toggle')
```
 

### *.modal('show')*
Manually opens a modal. **Returns to the caller before the modal has actually been shown** (i.e. before the `shown.bs.modal` event occurs).
```
$('#myModal').modal('show')

```


### *.modal('hide')*
Manually hides a modal. *Returns to the caller before the modal has actually been hidden* (i.e. before the hidden.bs.modal event occurs).
```
$('#myModal').modal('hide')
```

### *.modal('handleUpdate')*
Readjusts the modal's positioning to counter a scrollbar in case one should appear, which would make the modal jump to the left.

Only needed when the height of the modal changes while it is open.
```
$('#myModal').modal('handleUpdate')
```


## Events
Bootstrap's modal class exposes a few events for hooking into modal functionality.

All modal events are fired at the modal itself (i.e. at the `<div class="modal">`).

<table class="table table-bordered table-striped bs-events-table" style="margin: 0;">
  <thead>
   <tr>
     <th>Event Type</th>
     <th>Description</th>
   </tr>
  </thead>
  <tbody>
   <tr>
     <td>show.bs.modal</td>
     <td>This event fires immediately when the <code>show</code> instance method is called. If caused by a click, the clicked element is available as the <code>relatedTarget</code> property of the event.</td>
   </tr>
   <tr>
     <td>shown.bs.modal</td>
     <td>This event is fired when the modal has been made visible to the user (will wait for CSS transitions to complete). If caused by a click, the clicked element is available as the <code>relatedTarget</code> property of the event.</td>
   </tr>
   <tr>
     <td>hide.bs.modal</td>
     <td>This event is fired immediately when the <code>hide</code> instance method has been called.</td>
   </tr>
   <tr>
     <td>hidden.bs.modal</td>
     <td>This event is fired when the modal has finished being hidden from the user (will wait for CSS transitions to complete).</td>
   </tr>
   <tr>
     <td>loaded.bs.modal</td>
     <td>This event is fired when the modal has loaded content using the <code>remote</code> option.</td>
   </tr>
  </tbody>
</table>

```
$('#myModal').on('hidden.bs.modal', function (e) {
  // do something...
})
```




