# Mapbox GL Generic Geocoder

Bring your own geocoding service to [maplibre-gl-js](https://github.com/maplibre/maplibre-gl-js).  Based on [Mapbox GL Geocoder](https://github.com/mapbox/mapbox-gl-geocoder/)

## Example
```js
var geocodeNominatimRequest = function(query, mapBounds, options) {
	var params = { format: "json", q: query, limit: options.limit };
	var urlParams = new URLSearchParams(Object.entries(params));

	return fetch("http://nominatim.openstreetmap.org/search?" + urlParams).then(function(response) {
		if(response.ok) {
			return response.json();
		} else {
			return [];
		}
	}).then(function(json) {
		return json.map(function(result) {
			return {
				name: result.display_name,
				lat: result.lat,
				lon: result.lon,
				bbox: [result.boundingbox[2], result.boundingbox[0], result.boundingbox[3], result.boundingbox[1]]
			};
		});
	});
};

maplibremap.addControl(new MaplibreGenericGeocoder({}, geocodeNominatimRequest));
```

## Usage with a module bundler

This module exports a single class called MaplibreGenericGeocoder as its default export,
so in browserify or webpack, you can require it like:

```js
var MaplibreGenericGeocoder = require('maplibre-gl-generic-geocoder');
```
