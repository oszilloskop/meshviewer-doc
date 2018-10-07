# Map layers

Examples of GeoJSON as Promise. the split between json and option is form leaflet implementation. Multiple geo implementations are supported.

{% method %}
### Single Object

```js
geo: [
  {
	json: function () {
	  return Promise.resolve({
		'type': 'Feature',
		'geometry': {
		  'type': 'Polygon',
		  'coordinates': [
			[
			  [
				12.04925537109375,
				49.036517514836994
			  ],
			  [
				12.033462524414062,
				49.021660359632115
			  ],
			  [
				12.058181762695312,
				48.99553703238219
			  ],
			  [
				12.11311340332031,
				49.001843917978526
			  ],
			  [
				12.122726440429686,
				49.03381654386847
			  ],
			  [
				12.04925537109375,
				49.036517514836994
			  ]
			]
		  ]
		}
	  });
	},
	option: {
	  style: {
		color: '#e23535',
		weight: 5,
		opacity: 0.4,
		fillColor: '#6de922',
		fillOpacity: 0.1
	  }
	}
  }
]
```

{% endmethod %}

{% method %}
### Multi object

```js
geo: [
  {
	json: function () {
	  return Promise.all([
		  {
			  'type': 'Feature',
			  'geometry': {
				'type': 'Polygon',
				'coordinates': [
				  [
					[
					  12.04925537109375,
					  49.036517514836994
					],
					[
					  12.033462524414062,
					  49.021660359632115
					],
					[
					  12.058181762695312,
					  48.99553703238219
					],
					[
					  12.11311340332031,
					  49.001843917978526
					],
					[
					  12.122726440429686,
					  49.03381654386847
					],
					[
					  12.04925537109375,
					  49.036517514836994
					]
				  ]
				]
			  }
			}, {
			  'type': 'Feature',
			  'geometry': {
				'type': 'Polygon',
				'coordinates': [
				  [
					[
					  11.04925537109375,
					  49.036517514836994
					],
					[
					  12.033462524414062,
					  49.021660359632115
					],
					[
					  12.058181762695312,
					  48.99553703238219
					],
					[
					  12.11311340332031,
					  49.001843917978526
					],
					[
					  12.122726440429686,
					  50.03381654386847
					],
					[
					  12.04925537109375,
					  49.036517514836994
					]
				  ]
				]
			  }
			}
		]);
	},
	option: {
	  style: {
		color: '#e23535',
		weight: 5,
		opacity: 0.4,
		fillColor: '#6de922',
		fillOpacity: 0.1
	  }
	}
  }
]
```

{% endmethod %}


{% method %}
### Dynamic/Ajax objects
```js
geo: [
      {
        json: function () {
          var linkScale = require('d3-interpolate').interpolateHslLong('darkblue', 'darkred');

          return require('helper').getJSON('https://opendata.ffggrz.de/').then(function (result) {
            result.features.forEach(function (item) {
              var temp = ((item.properties.temperature ? item.properties.temperature.toString() : 0) + 20) / 55;
              item.color = linkScale(temp);
            });

            return result.features ? result.features : false;
          }, function () {
            return false;
          });
        },

        option: {
          pointToLayer: function (feature, latlng) {
            return L.circleMarker(latlng, {
              radius: 8,
              fillColor: feature.color,
              color: '#000',
              weight: 1,
              opacity: 1,
              fillOpacity: 0.8
            }).bindTooltip(feature.properties.temperature ? 'Temperatur: ' + feature.properties.temperature.toString() + 'C' : '');
          },
          pane: 'markerPane'
        }
      }
    ]
```
https://github.com/d3/d3-interpolate#color-spaces - Info about colors

{% endmethod %}
