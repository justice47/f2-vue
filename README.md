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
	:geometry="geometry"
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

![Charts](https://user-images.githubusercontent.com/29502063/67677996-8b5c3f80-f996-11e9-838c-e5bffa0abb13.PNG)

### Example with some props

```
<f2chart
	:data="data"
	:geometry="geometry"
	:width="500"
	:height="200"
	:scale="scale"
	:coord="coord"
	:tooltip="tooltip"
	:legend="false"
	:guide="guide"
	:scrollBar="scrollBar"
	ref="chart"
/>
```

```
export default {
 return {
		data: [
			{ year: "1951", sales: 38 },
			{ year: "1952", sales: 52 },
			{ year: "1956", sales: 61 },
			{ year: "1957", sales: 145 },
			{ year: "1958", sales: 48 },
			{ year: "1959", sales: 38 },
			{ year: "1960", sales: 38 },
			{ year: "1962", sales: 47 }
		],
		geometry: [
			{
				type: "interval",
				position: ["year", "sales"],
				color: 'year',
				animation: false
			},
			{
				type: "line",
				position: ["year", "sales"],
			}
		],
		scale: [
			{
				field: "sales",
				config: {
				min: 0,
				max: 300
				}
			}
		],
		coord: {
			type: "rect",
			config: {
				transposed: false
			}
		},
		axis: [
			{
				field: "",
				config: {}
			}
		],
		legend: false,
		tooltip: {
			alwaysShow: true,
		},
		guide: [
		  	{
				type: 'line',
				config: {
					start: ['min', 175],
					end: ['max', 175],
					style: {
						lineWidth: 2,
						stroke: 'red'
					}
				}
		  	}
		],
		scrollBar: {
		 mode: 'x',
			xStyle: {
			  offsetY: -5
			}
		}
	}
}
```

![Charts3](https://user-images.githubusercontent.com/29502063/67678557-efcbce80-f997-11e9-926d-7bcf60952999.PNG)

## Issues and contributing

Feel free to submit an issue or the PR
