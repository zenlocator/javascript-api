
# ZenLocator JavaScript API

This is the official documentation for the client-side [ZenLocator](https://zenlocator.com/) JavaScript API. You must have an account on [ZenLocator](https://zenlocator.com/) and use one of the widgets (map, locator, search, etc) on your website in order to use the code in this documentation.

The documentation is always for the latest version of ZenLocator JavaScript API. Your widgets are automatically updated as we push new code changes. If you'd like to ensure backwards compatibility with your custom integration, consider freezing your automatic updates by going to **Account** > **Settings** > **Automatic Updates** on your [ZenLocator dashboard](https://app.zenlocator.com/) and turning that setting **off**. Then when you're ready to update your SDK, you can manually update to the latest version.

## Usage

This is an example setup for your maps widget:

```html
<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js" async></script>
```

The JavaScript API & SDK is already included in the code above. Once your script loads, you will have access to all of the methods and events outlined below.

## Callback

By passing the `callback` parameter to your script you have the ability to be notified when the global ZenLocator object is available for use:

```html
<script type="text/javascript">
  window.zenlocatorInit = function(widget, type) {
    if (type === 'map') {
      console.log('your map widget has been initialized');
    }
  };
</script>

<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js?callback=zenlocatorInit" async></script>
```

Otherwise, you can also watch for the global `window.zenlocator.map` object that is automatically created on your website.

## Methods

The following methods are available on your widget objects (`window.zenlocator.map`, `window.zenlocator.directory`, etc) once the code has been initialized. Scroll down for more examples.

| Method           | Description                                                        | Example Usage                                                                                          |
| ---------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `getLocations()` | Gets all the locations that have been loaded on the widget.        | `var locations = widget.getLocations();`                                                               |
| `getMarkers()`   | Gets all the marker objects.                                       | `var markers = widget.getMarkers();`                                                                   |
| `getProducts()`  | Gets all the products.                                             | `var products = widget.getProducts();`                                                                 |
| `getFilters()`   | Gets all the filters.                                              | `var filters = widget.getFilters();`                                                                   |
| `getRetailers()` | Gets all the retailers.                                            | `var retailers = widget.getRetailers();`                                                               |
| `getLanguage()`  | Get the language object loaded for the current visitor/browser.    | `var language = widget.getLanguage();`                                                                 |
| `getHours()`     | Gets the array of hours objects.                                   | `var hours = widget.getHours();`                                                                       |
| `on(event, fn)`  | Adds a listener for the `event` that will trigger a function `fn`. | `widget.on('LOCATION_OPENED', (data) => console.log('you have opened location '+data.location.name);`  |
| `off(event, fn)` | Removes the listener added by `on(event, fn)`.                     | `widget.off('LOCATION_OPENED', (data) => console.log('you have opened location '+data.location.name);` |

## Events

This is a list of events your code can listen to by using the `.on(event, fn)` method. You can also remove these listeners by providing the same arguments to `.off(event, fn)`.

| Event Name            | Description                                                                                                                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LOCATION_OPENED`     | Location has either been opened by user or by widget's settings (auto-open). The function parameters will contain the location object.                                                       |
| `SEARCH_LOCATIONS`    | A search has been done. The function parameters will contain the search query, as well as additional search parameters (like radius, filters and products) as well as the number of results. |
| `BUTTON_CLICK`        | Location button has been clicked. The data will contain location and button details.                                                                                                         |
| `CONTACT_CLICK`       | Location contact info has been clicked. The data will contain location and contact details.                                                                                                  |
| `BROWSER_GEOLOCATION` | Browser gelocation has been triggered after the user has allowed it. The data will contain coordinates as well as an approximate address.                                                    |
| `MAP_MAXIMIZED`       | Map widget has been maximized.                                                                                                                                                               |
| `MAP_MINIMIZED`       | Map widget has been minimized.                                                                                                                                                               |
| `MAP_ZOOMED_IN`       | Map has been zoomed in.                                                                                                                                                                      |
| `MAP_ZOOMED_OUT`      | Map has been zoomed out.                                                                                                                                                                     |

## Examples

Getting a list of locations after the search:

```html
<script type="text/javascript">
  window.zenlocatorInit = function(widget, type) {
    if (type === 'map') {
      widget.on('SEARCH_LOCATIONS', (data) => {
        var locations = widget.getLocations();
        console.log(`there's ${locations.length} locations in "${data.query}"`);
      });
    }
  };
</script>

<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js?callback=zenlocatorInit" async></script>
```

Triggering an action every time a location is viewed/opened:

```html
<script type="text/javascript">
  window.zenlocatorInit = function(widget, type) {
    if (type === 'map') {
      widget.on('LOCATION_OPENED', (data) => {
        console.log(`you've opened location "${data.location.name}"`);
      });
    }
  };
</script>

<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js?callback=zenlocatorInit" async></script>
```

Trigger an action every time a button has been clicked on a location:

```html
<script type="text/javascript">
  window.zenlocatorInit = function(widget, type) {
    if (type === 'map') {
      widget.on('BUTTON_CLICK', (data) => {
        console.log(`you've clicked the "${data.button.name}" button on location "${data.location.name}"`);
      });
    }
  };
</script>

<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js?callback=zenlocatorInit" async></script>
```

## Questions

For questions, comments or general feedback, please email [support@zenlocator.com](mailto:support@zenlocator.com)
