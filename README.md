# f2-vue
Vue component for elegant, interactive and flexible mobile chart library

Original library - [antvis/f2](https://github.com/antvis/f2 "antvis/f2")

## Roadmap

✅ Basic functionality  
✅ Chart instance settings  
✅ Geometry  
✅ Scale  
✅ Coord  
✅ Axis  
✅ Legend  
✅ Guide  
✅ Scrollbar  
✅ Rerender on data change  

⚠️ Util methods  
⚠️ Context  
⚠️ All the methods besides first render

## Installation

```bash
$ npm install f2-vue
```
## Import
```
import f2chart from "f2-vue";
```
```
export default {
  components: {
    f2chart
  }
},
```
```
<f2chart />
```
## Docs
You can find full API for F2 chart here: [API for F2](https://antv.gitbook.io/f2/api/ "API for F2")  
Pay attention to the [Roadmap](#Roadmap "Roadmap") section of this page - there is actual list of working features.
### Basic example
```
<f2chart
	:data="data"
	:geometry="geometry
	ref="chart"
/>
```
```
export default {
	return {
		data: [
			{ year: "1951", sales: 38 },
			{ year: "1952", sales: 52 },
			{ year: "1956", sales: 61 }
		],
			geometry: [
			{
			  type: "interval",
			  position: ["year", "sales"],
			  color: 'year'
			}
		],
	}
}
```