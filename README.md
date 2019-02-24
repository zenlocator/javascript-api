
# ZenLocator JavaScript API

This is the official documentation for the client-side [ZenLocator](https://zenlocator.com/) widget API. You must have an account on [ZenLocator](https://zenlocator.com/) and use one of the widgets (map, locator, search, etc) on your website in order to use the code in this documentation.

## Usage

Here is an example setup for your maps widget:

```html
<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js" async></script>
```

The JavaScript API & SDK is already included in the code above. Once your script loads, you will have access to all the methods and events outlined below.

## Callback

By passing the `callback` parameter to your script you have the ability to be notified when the ZenLocator object is available for use:

```html
<script type="text/javascript">
  window.zenlocatorLoaded = function(widget, type) {
    if (type === 'map') {
      console.log('your map widget has been initialized');
	}
  };
</script>

<div id="zenlocator-map-j48f89jq"></div>
<script type="text/javascript" src="https://js.zenlocator.com/ys9ydfx2.min.js?callback=zenlocatorLoaded" async></script>
```

Otherwise, you can also watch for the global `window.zenlocator` object that is automatically created on your website.

## Methods

| Method         | Description                                                        | Example Usage                                                                                          |
| -------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| getLocations() | Gets all locations that have been loaded to the widget.            | `var locations = widget.getLocations();`                                                               |
| getMarkers()   | Gets all the marker objects.                                       | `var markers = widget.getMarkers();`                                                                   |
| getProducts()  | Gets all the products.                                             | `var products = widget.getProducts();`                                                                 |
| getFilters()   | Gets all the filters.                                              | `var filters = widget.getFilters();`                                                                   |
| getRetailers() | Gets all the retailers.                                            | `var retailers = widget.getRetailers();`                                                               |
| getLanguage()  | Get the language object loaded for the current visitor/browser.    | `var language = widget.getLanguage();`                                                                 |
| getHours()     | Gets the array of hours objects.                                   | `var hours = widget.getHours();`                                                                       |
| on(event, fn)  | Adds a listener for the `event` that will trigger a function `fn`. | `widget.on('LOCATION_OPENED', (data) => console.log('you have opened location '+data.location.name);`  |
| off(event, fn) | Removes the listener added by `on(event, fn)`.                     | `widget.off('LOCATION_OPENED', (data) => console.log('you have opened location '+data.location.name);` |

## Events

The following is a list of events your code can listen to using the `.on(event, fn)`:

| Event Name            | Description                                                                                                                                                                           | Example Usage                                                                                         |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `LOCATION_OPENED`     | Location has either been opened by user or by widget's settings (auto-open). The data will contain location details.                                                                  | `widget.on('LOCATION_OPENED', (data) => console.log('you have opened location '+data.location.name);` |
| `SEARCH_LOCATIONS`    | A search has been done. The data will contain the search query, as well as additional search parameters (like radius, filters and products) as well as the number of found locations. |                                                                                                       |
| `BUTTON_CLICK`        |                                                                                                                                                                                       |                                                                                                       |
| `CONTACT_CLICK`       |                                                                                                                                                                                       |                                                                                                       |
| `BROWSER_GEOLOCATION` |                                                                                                                                                                                       |                                                                                                       |
| `MAP_MAXIMIZED`       |                                                                                                                                                                                       |                                                                                                       |
| `MAP_MINIMIZED`       |                                                                                                                                                                                       |                                                                                                       |
| `MAP_ZOOMED_IN`       |                                                                                                                                                                                       |                                                                                                       |
| `MAP_ZOOMED_OUT`      |                                                                                                                                                                                       |                                                                                                       |
