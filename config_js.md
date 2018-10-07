# Configuration

Gulp merges `config.js` into `config.default.js` (`config.default.js` will be overwritten). **This is no deep merge**, i.e. you always need to add **complete** arrays or objects like `nodeInfobox` or `supportedLocale` to your `config.js`. You can use JS and functions to create new node details rows.

> **`config.default.js`** contains settings like `supportedLocale` or `maxAge`
> **`config.js`** contains community specific settings like statistic images or `siteName` (and the values/arrays/objects you want to overwrite in config.default.js)

## config.js

{% method %}
### dataPath (string/array)
`dataPath` needs a path/URL with `meshviewer.js` provided in an array. Don't forget the trailing slash!
Also, proxying the data through a webserver will allow `brotli` or `deflat/gzip` which will greatly reduce bandwidth consumption. The header `Access-Control-Allow-Origin: "*"` should be added to allow local development.

{% sample lang="js" %}
Single data source
```js
'dataPath' : [
    'https://regensburg.freifunk.net/data/'
]
```

Multiple data sources
```js
'dataPath' : [
    'https://regensburg.freifunk.net/data/',
    'https://bremen.freifunk.net/data/'
]
```
{% endmethod %}


{% method %}
### siteName (string)
Set this to match your community name. It's used in several places.

{% sample lang='js' %}
```js
'siteName': 'Freifunk Regensburg'
```
{% endmethod %}

### mapLayers (List)

A list of objects describing the map layers. Each object has at least the properties `name`, `url` and `config`.

- A list of some possible layers available: [Example layers and configuration](http://leaflet-extras.github.io/leaflet-providers/preview/), but every source supporting the used standard will work.
- [Layer provider list for meshviewer](/build_install/map-layers.md)

{% method %}
#### mode (string, optional)

Allows to load an additional style for a night mode or a similar use case. It is possible to load the stylesheet `inline` or with a `link`-tag. 
Inline avoids re-rendering and possible issues with label-layer updates. It is important to add the following attributes: `class="css-mode mode-name" media="not"`.

_Default mode is `night` which is added inline in `index.html`_

{% sample lang='js' %}
```js
'mode': 'night'
```

`html/index.html`
```html
 <link rel="stylesheet" class="css-mode mode-name" media="not" href="mode-name.css">
```

or

```html
<style class="css-mode mode-name" media="not">
   <inline src="mode-name.css" />
</style>
```
{% endmethod %}


{% method %}
#### start (integer, optional)

Start a time range to put this mapLayer on first position.
{% sample lang='js' %}
```js
'start': 19
```
{% endmethod %}


{% method %}
#### end (integer, optional)

End a time range for first map. Stops sort this mapLayer.

{% sample lang='js' %}
```js
'end': 7
```
{% endmethod %}


{% method %}
### fixedCenter (array[array, array])

This sets the initial area shown on loading the map. Chose exactly two locations. Everything between those two locations will be displayed. Nodes outside the initial `fixedCenter`` will be visible then you use map controls like zoom or moving around on the map.

{% sample lang='js' %}
Examples for `fixedCenter`:

```js
'fixedCenter': [
  [
    49.3522,
    11.7752
  ],
  [
    48.7480,
    12.8917
  ]
],
```
{% endmethod %}


{% method %}
### nodeInfos (array, optional)

This option allows to show node statistics depending on following case-sensitive parameters:

- `name` - header of statistics segment in the infobox
- `href` - absolute or relative URL to statistics image
- `image` **(required)** - absolute or relative URL to image,
  can be the same like `href`
- `title` - the image title tag (also used as mouse hover)

To insert variables in either `href`, `image` or `title` you can use the case-sensitive template strings `{NODE_ID}`, `{NODE_NAME}`, `{LOCALE}` and `{TIME}` (as cache-breaker).

{% sample lang='js' %}
Examples for `nodeInfos`:

```js
'nodeInfos': [
  { 
    'name': 'Clientstatistik',
    'href': 'stats/dashboard/db/node-byid?var-nodeid={NODE_ID}',
    'image': 'stats/render/dashboard-solo/db/node-byid?panelId=1&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&var-host={NODE_NAME}&_t={TIME}',
    'title': 'Knoten {NODE_ID}'
  },
  {
    'name': 'Uptime',
    'href': 'stats/dashboard/db/node-byid?var-nodeid={NODE_ID}',
    'image': 'stats/render/dashboard-solo/db/node-byid?panelId=2&fullscreen&theme=light&width=600&height=300&var-nodeid={NODE_ID}&_t={TIME}',
    'title': 'Knoten {NODE_ID}'
  }
]
```

In order to have statistics images available, you have to set up an instance of each [Prometheus](http://prometheus.io/) and [Grafana](http://grafana.org/).
{% endmethod %}


{% method %}
### globalInfos (array, optional)

This option allows to show global statistics on statistics page depending on following case-sensitive parameters:

- `name` - header of statistics segment in the infobox
- `href` - absolute or relative URL to statistics image
- `image` **(required)** - absolute or relative URL to image,
  can be the same like `href`
- `title` - the image title tag (also used as mouse hover)

To insert the variables locale or time (as cache-breaker) in either `href`, `image` or `title`
you can use the case-sensitive template strings `{LOCALE}` and `{TIME}`.


{% sample lang='js' %}
Examples for `globalInfos` using Grafana server rendering:

```js
'globalInfos': [
  { 
    'name': 'Wochenstatistik',
    'href': 'stats/render/render/dashboard-solo/db/global?panelId=1&fullscreen&theme=light&width=600&height=300',
    'image': 'nodes/globalGraph.png',
    'title': 'Bild mit Wochenstatistik'
  }
]
```
{% endmethod %}


{% method %}
### linkInfos (array, optional)

This option allows to show link statistics depending on the following case-sensitive parameters:

- `name` - header of statistics segment in the infobox
- `href` - absolute or relative URL to statistics image
- `image` **(required)** - absolute or relative URL to image,
  can be the same like `href`
- `title` - the image title tag (also used as mouse hover)

To insert the source or target variables in either `href`, `image` or `title`
you can use the case-sensitive template strings `{SOURCE_ID}`, `{TARGET_ID}`, `{SOURCE_MAC}`, `{TARGET_MAC}`, `{SOURCE_ADDR}`, `{TARGET_ADDR}`, `{SOURCE_NAME}`, `{TARGET_NAME}`, `{LOCALE}` and `{TIME}` (as cache-breaker).

{% sample lang='js' %}
```js
'linkInfos': [
  {
    'name': 'Linkstatistik',
    'href': 'stats/dashboard/db/links?var-source={SOURCE_ID}&var-target={TARGET_ID}',
    'image': 'stats/render/dashboard-solo/db/links?panelId=1&fullscreen&theme=light&width=800&height=600&var-source={SOURCE_ID}&var-target={TARGET_ID}&_t={TIME}',
    'title': 'Bild mit Linkstatistik'
  }
]
```
{% endmethod %}


{% method %}
### siteNames (array, optional)

In this array name definitions for site statistics and node info can be set. This requires one object for each `site` code. This object must contain:

- `site` - the site code
- `name` - the displayed name for this site

If neither `siteNames` nor `showSites` are set, site statistics and node info won't be displayed.

{% sample lang='js' %}
Example for `siteNames`:

```js
  'siteNames': [
    {
      'site': 'ffrgb',
      'name': 'Regensburg'
    },
    {
      'site': 'ffrgb-dummy',
      'name': 'Regensburg Test'
    }
  ]
```
{% endmethod %}

{% method %}
### linkList (array, optional)

Defines an additional list of links displayed in the infobox. It can be used for links to legal notice, web or stats:

- `title` - the image title tag (also used as mouse hover) link
- `href` - URL of the link

{% sample lang='js' %}
Example for `linkList`:

```js
    'linkList': [
      {
        'title': 'Impressum',
        'href': '/verein/impressum/'
      },
      {
        'title': 'Datenschutz',
        'href': '/verein/datenschutz/'
      }
    ]
]
```
{% endmethod %}

{% method %}
### geo (array, optional)

The definition for additional custom GeoJSON objects to be displayed in Meshviewer.

- `json` - geoJSON (javascript allowed e.g. load external json)
- `option` - style or other options

[Multiple GeoJSON examples](examples/geo-json.md)

{% sample lang='js' %}
Example for `geo`:

```js
geo: [
      {
        json: function () {
          return Promise.all([
              // Content
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

## config.default.js

{% method %}
### reverseGeocodingApi (string)
Settings for a reverse proxy or your own geocoding server used by the location-picker. Setting up this will enhance data privacy and avoid problems caused by script-blockers like NoScript in case you are using different domains for your json data or the map tiles. External URLs need to be considered in your privacy policy.

{% sample lang='js' %}
```js
'reverseGeocodingApi': 'https://nominatim.openstreetmap.org/reverse'
```
{% endmethod %}


{% method %}
### maxAge (string)
Nodes being online for less than `maxAge` days are considered "new". Likewise,
nodes being offline for more than than `maxAge` days are considered "lost".

{% sample lang='js' %}
```js
'maxAge': 14
```
{% endmethod %}


{% method %}
### maxAgeAlert (integer)
Nodes being offline for more than than `maxAge` days are considered "lost".
Lost will be split up in `alert` and `lost`.

{% sample lang='js' %}
```js
'maxAgeAlert': 3
```
{% endmethod %}


{% method %}
### nodeZoom (integer)
The zoom level that is used when clicking on a node or when using a deep-link URL directly to a node. The value `18` is a good default where nearby buildings and streets should be visible.

{% sample lang='js' %}
```js
'nodeZoom': 18
```
{% endmethod %}


{% method %}
### labelZoom (integer)
Min. zoom level from which on the node labels are shown on the map. Note that every level in between `labelZoom` and `maxZoom` (defined in `mapLayers`) has a negative performance impact.

{% sample lang='js' %}
```js
'labelZoom': 13
```
{% endmethod %}


{% method %}
### clientZoom (integer)
The min. level from which on the client dots are visible. Note that every level in between `clientZoom` and `maxZoom` (defined in `mapLayers`) has a negative performance impact.

{% sample lang='js' %}
```js
'clientZoom': 15
```
{% endmethod %}


{% method %}
### nodeAttr (array)
Remove or add node properties in details view. The value can be a node attribute (depth 1) or any of the functions with a name starting with "show" from `lib/utils/node.js`.

{% sample lang='js' %}
```js
'nodeAttr': [
    // value can be a node attribute (depth 1) or any of the functions with a name starting with "show" from lib/utils/node.js with
    {
      'name': 'node.status',
      'value': 'Status'
    },
    {
      'name': 'node.gateway',
      'value': 'Gateway'
    },
    {
      'name': 'node.coordinates',
      'value': 'GeoURI'
    },
// Remove unwanted attributes    
//    {
//      'name': 'node.contact',
//      'value': 'owner'
//    },
    {
      'name': 'node.hardware',
      'value': 'model'
    },
    {
      'name': 'node.primaryMac',
      'value': 'mac'
    },
    {
      'name': 'node.firmware',
      'value': 'Firmware'
    },
    {
      'name': 'node.uptime',
      'value': 'Uptime'
    },
    {
      'name': 'node.firstSeen',
      'value': 'FirstSeen'
    },
    {
      'name': 'node.systemLoad',
      'value': 'Load'
    },
    {
      'name': 'node.ram',
      'value': 'RAM'
    },
    {
      'name': 'node.ipAddresses',
      'value': 'IPs'
    },
    {
      'name': 'node.update',
      'value': 'Autoupdate'
    },
    {
      'name': 'node.site',
      'value': 'Site'
    },
    {
      'name': 'node.clients',
      'value': 'Clients'
    }
  ]
```
{% endmethod %}


{% method %}
### supportedLocale (array)
Add supported locale (with matching language file in `locales/*.js`). This will be matched against the browser language setting. Fallback will be the first language in the array.

{% sample lang='js' %}
Example for `supportedLocale`:

```js
'supportedLocale': [
  'en',
  'de',
  'cz',
  'fr',
  'tr',
  'ru'
]
```
{% endmethod %}


{% method %}
### color (array)
Different color values for all canvas related settings. Couldn't be done via SCSS.

{% endmethod %}


{% method %}
### cacheBreaker (string)
Will be replaced in every build to avoid missing or outdated language strings because `language.js` is not up to date.

_Fixed value (vy0zx)._
{% endmethod %}
