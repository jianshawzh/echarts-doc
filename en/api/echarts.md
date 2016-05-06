{{ target: echarts }}
# echarts(Object)

Global echarts bject，can be obtained by introducing `echarts.js` in script label or through  `require('echarts')` in AMD environment.

## init(Function)
```js
(dom: HTMLDivElement|HTMLCanvasElement, theme?: Object|string, opts?: {
    devicePixelRatio?: number
    renderer?: string
}) => ECharts
```
Create a ECharts example，go back to [echartsInstance](~echartsInstance)，but you can not initialize multiple ECharts examples on a single container.

**parameter**
+ `dom`

    Example container, usually is an element `div` with height and width. 

    **Attention：**if `div` is hidden, ECharts is likely to fail initializing, then you can explicitly specified `style.width` and `style.height` of `div`, or manually adjust sizes of [echartsInstance.resize](echartsInstance.resize) after showing `div`.

    ECharts 3 supports using `canvas` element as container directly, thus canvas can be applied somewhere elses as pictures directly after completing chart, for example, canvas can be used as map in WebGL, compared to picture links generated by using  [echartsInstance.getDataURL](~echartsInstance.getDataURL) ,this supports hourly update of charts.

+ `theme`

    Theme applied.This can be a configuration object of a theme, or a theme name registered through [echarts.registerTheme](~echarts.registerTheme).

+ `opts`

    Attached parameter.There are several options below:

    + `devicePixelRatio`

       Device pixels, take browser values `window.devicePixelRatio` by default.

    + `renderer`

        The renderer only supports `'canvas'` by now.

## connect(Function)
```js
(group:string|Array)
```

Multiple examples of the graph realize linkage.

**parameter：**
+ `group`
    group id，or array of chart example.

**For example：**
```js
// set group id of each example respectively.
chart1.group = 'group1';
chart2.group = 'group1';
echarts.connect('group1');
// or incoming example array that need to be linked.
echarts.connect([chart1, chart2]);
```

## disConnect(Function)
```js
(group:string)
```
Disconnect chart example. If only a single example need to be removed,  you can set this chart example `group` to empty.

**parameter：**
+ `group`

    group id.

## dispose(Function)
```js
(target: ECharts|HTMLDivElement|HTMLCanvasElement)
```
Destroy example, this example will not be able to used once destroyed.

## getInstanceByDom(Function)
```js
(target: HTMLDivElement|HTMLCanvasElement) => ECharts
```
Obtain example from dom container.

## registerMap(Function)
```js
(mapName: string, geoJson: Object, specialAreas?: Object)
```
Register maps that are available, which can only be used when it includes [geo](option.html#geo) component or  chart category of [map](option.html#series-map).

Ways of usage can refer to [option.geo](option.html#geo.map)。

**parameter：**
+ `mapName`

    Map name， `map` set in [geo](option.html#geo) component or [map](option.html#series-map)chart category is value concerned.

+ `geoJson`

    Data if GeoJson format，specific format can refer to [http://geojson.org/](http://geojson.org/).

+ `specialAreas`

    Options.Zoom part of areas in the map to suitbable location can make the whole map look better. 

    **For example [USA Population Estimates](${galleryEditorPath}map-usa)：**
    ```js
echarts.registerMap('USA', usaJson, {
    // Move Alaska to the bottom left of United States 
    Alaska: {
        // Upper left longitude
        left: -131,
        // Upper left latitude
        top: 25,
        // Range of longitude 
        width: 15
    },
    // Hawaii
    Hawaii: {
        left: -110,
        top: 28,
        width: 5
    },
    // Puerto Rico
    'Puerto Rico': {
        left: -76,
        top: 26,
        width: 2
    }
});
    ```


## registerTheme(Function)
```js
(themeName: string, theme: Object)
```

register theme, which is specified when[initialize example](~echarts.init).