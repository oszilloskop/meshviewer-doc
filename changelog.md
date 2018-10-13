# Changelog

## 11.0.0
* [TASK] Use Promises for GeoJSON
* [TASK] Update packages & add SHA integrity
* **[TASK] Replace site with domain**
* **[TASK] Libary updates gulp4**
* **[TASK] Prevent XSS in tooltip**
* [TASK] Remove unnecessary moment
* [TASK] Remove obsolete windows, rename macosx to osx
* [TASK] Remove bithound
* [TASK] Remove localStorage
* **[TASK] Add dynamic title to offline html and multiple metatags**
* **[TASK] Add optional fullscreen mode**
* **[TASK] Add GeoJSON support**
* [TASK] Improve night colors
* **[!!!][TASK] Indexable urls**
* [BUGFIX] URL router can fail at high load
* [TASK] Update github issue templates
* [TASK] Add nodejs 10 and remove 9 from travis
* [TASK] Move to v8 promies polyfill & eslint5
* **[TASK] Add posibility for links DSGVO** und natürlich auch andere
* **[TASK] Add OpenGraph, twitter card & Microdata + Favicon update**
* **[TASK] Add simple offline service worker**
* **[TASK] Add source/target address to link variables**
* [BUGFIX] Bar width max 100%
* **[BUGFIX] Allow negative coordinates**
* **[BUGFIX] Correct filled loadavg bar with nproc > 1**
* **[TASK] Show rectangle gateway in forcegraph**
* **[TASK] Show offline nodes in forcegraph**
* [TASK] Upgrade to leaflet 1.3
* [TASk] Upgrade to navigo 7
* [Multiple minor libary updates like d3js](https://github.com/ffrgb/meshviewer/commits/v11.0.0)

### Additionally
* `multiple`-branch
	* Our test environment has now over 21500 nodes on a single map and still works  https://multi.meshviewer.org/
* We moved the docu, website, multi and develop instance - currently no auto builds on master branch
* Multiple changes on webhooks and tests like scrutinizer

**THX @all active and passed contributors!**
=======

## 10.0.0

* Performance improvements (critical path, avoid blocking code)
* Replaced router - including language, mode, node, link, location
* Leaflet upgraded to v1 - faster on mobile
* Forcegraph rewrite with d3.js v4
* Map layer modes \(Allow to set a default layer based on time combined with a stylesheet\)
* Automatic updates for selected node or list \(incl. image stats cache-breaker\)
* Node filter
* Zoom level for clicking on a node \(`nodeZoom`\) is definable independently from the maximum zoom level 22
* Formatted Code
* Translation support - Help to improve or add languages at [Online translation platform](https://poeditor.com/join/project/VZBjPNNic9)
  * Currently available: en, de, fr, cz, tk & ru
* Gulp inline for some css and js - fewer requests and instant load indicator
* Icon font with needed icons only
* Switch to Gulp \(Tested with Node.js 6 LTS, 8 on Linux, OSX & W\*\*\)
  * css and some js moved inline
* Yarn in favour of bower
  * Load only moment.js without languages \(Languages are included in translations\)
  * unneeded components removed \(es6-shim, tablesort, numeraljs, leaflet-providers, leaflet-label jshashes, chroma-js\)
* RBush v2 - performance boost in last versions \(positions, labels and clients on the map\)
* Ruby dependency removed
* FixedCenter is required
* Sass-lint, scss and variables rewritten for easy customizations/adjustments
* Cross browser/device support improved \(THX@BrowserStack\)
* Yarn package manager in favour of npm
* Configurable reverse geocoding server
* Split clients into 2,4, 5Ghz and others
* Show nexthop and gateways \(IPv4/IPv6\)
* Dynamic node detail attributes
* Config inheritance and functions
* Dynamic map center (sidebar toggle)
* Show connection type (icon)
^ Accessibility improvements
* Few Internet Explorer 11 fixes
* Necessary polyfills - no overhead
* **Switch to meshviewer.json - less depth, new informations**
<<<<<<< Updated upstream
* [A lot more in the commit history](https://github.com/ffrgb/meshviewer/commits/master)
=======
* [A lot more in the commit history](https://github.com/ffrgb/meshviewer/commits/v10.0.0)
>>>>>>> Stashed changes



