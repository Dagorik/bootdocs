@page javascript-overview Overview
@parent javascript 1

## Individual or compiled
Plugins can be included individually (using Bootstrap's individual `*.js files`), or all at once (using `bootstrap.js` or the minified `bootstrap.min.js`).

### Using the compiled JavaScript
Both `bootstrap.js` and `bootstrap.min.js` contain all plugins in a single file. Include only one.

### Plugin dependencies
Some plugins and CSS components depend on other plugins. If you include plugins individually, make sure to check for these dependencies in the docs. Also note that all plugins depend on jQuery (this means jQuery must be included before the plugin files). Consult our `bower.json` to see which versions of jQuery are supported.

## Data attributes
You can use all Bootstrap plugins purely through the markup API without writing a single line of JavaScript. This is Bootstrap's first-class API and should be your first consideration when using a plugin.

That said, in some situations it may be desirable to turn this functionality off. Therefore, we also provide the ability to disable the data attribute API by unbinding all events on the document namespaced with `data-api`. This looks like this:

```
$(document).off('.data-api')
```

Alternatively, to target a specific plugin, just include the plugin's name as a namespace along with the data-api namespace like this:

```
$(document).off('.alert.data-api')
```
### Only one plugin per element via data attributes
Don't use data attributes from multiple plugins on the same element. For example, a button cannot both have a tooltip and toggle a modal. To accomplish this, use a wrapping element.

## Programmatic API
We also believe you should be able to use all Bootstrap plugins purely through the JavaScript API. All public APIs are single, chainable methods, and return the collection acted upon.
```
$('.btn.danger').button('toggle').addClass('fat')
```
All methods should accept an optional options object, a string which targets a particular method, or nothing (which initiates a plugin with default behavior):

```
$('#myModal').modal()                      // initialized with defaults
$('#myModal').modal({ keyboard: false })   // initialized with no keyboard
$('#myModal').modal('show')                // initializes and invokes show immediately
```
Each plugin also exposes its raw constructor on a Constructor property: `$.fn.popover.Constructor`. If you'd like to get a particular plugin instance, retrieve it directly from an element: `$('[rel="popover"]').data('popover')`.

#### Default settings

You can change the default settings for a plugin by modifying the plugin's Constructor.DEFAULTS object:

```
$.fn.modal.Constructor.DEFAULTS.keyboard = false // changes default for the modal plugin's `keyboard` option to false
```
## No Conflict
Sometimes it is necessary to use Bootstrap plugins with other UI frameworks. In these circumstances, namespace collisions can occasionally occur. If this happens, you may call `.noConflict` on the plugin you wish to revert the value of.

```
var bootstrapButton = $.fn.button.noConflict() // return $.fn.button to previously assigned value
$.fn.bootstrapBtn = bootstrapButton            // give $().bootstrapBtn the Bootstrap functionality
```

## Events
Bootstrap provides custom events for most plugins' unique actions. Generally, these come in an infinitive and past participle form - where the infinitive (ex. `show`) is triggered at the start of an event, and its past participle form (ex. `shown`) is triggered on the completion of an action.

As of 3.0.0, all Bootstrap events are namespaced.

All infinitive events provide `preventDefault` functionality. This provides the ability to stop the execution of an action before it starts.

```
$('#myModal').on('show.bs.modal', function (e) {
  if (!data) return e.preventDefault() // stops modal from being shown
})
```

## Version Numbers
The version of each of Bootstrap's jQuery plugins can be accessed via the `VERSION` property of the plugin's constructor. For example, for the tooltip plugin:

```
$.fn.tooltip.Constructor.VERSION // => "3.3.5"
```
## No special fallbacks when JavaScript is disabled
Bootstrap's plugins don't fall back particularly gracefully when JavaScript is disabled. If you care about the user experience in this case, use `<noscript>` to explain the situation (and how to re-enable JavaScript) to your users, and/or add your own custom fallbacks.

### Third-party libraries
Bootstrap does not officially support third-party JavaScript libraries like Prototype or jQuery UI. Despite  `.noConflict` and namespaced events, there may be compatibility problems that you need to fix on your own.
