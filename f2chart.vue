<template>
  <div>
    <canvas id="mountNode"></canvas>
  </div>
</template>

<script>
import F2 from "@antv/f2";
const ScrollBar = require('@antv/f2/lib/plugin/scroll-bar');
F2.Chart.plugins.register(ScrollBar); 

export default {
  name: "f2chart",
  props: {
    data: {
      type: Array,
      required: true
    },
    width: {
      type: [String, Number],
      default: null
    },
    height: {
      type: [String, Number],
      default: null
    },
    padding: {
      default: "auto"
    },
    appendPadding: {
      default: 15
    },
    pixelRatio: {
      type: Number,
      default: 1
    },
    animate: {
      type: Boolean,
      default: true
    },
    limitInPlot: {
      type: Boolean,
      default: false
    },
    geometry: {
      required: true
    },
    scale: {
      type: Array
    },
    coord: {
      type: Object
    },
    axis: {
      type: Array
    },
    legend: {
      type: [Object, Boolean, Array],
      default: true
    },
    tooltip: {
      type: Object
    },
    guide: {
      type: [Object, Array]
    },
    scrollBar: {
      type: Object
    }
  },
  data() {
    return {
      chart: {}
    };
  },
  mounted() {
    this.chart = new F2.Chart({
      id: "mountNode",
      width: this.width,
      height: this.height,
      padding: this.padding,
      appendPadding: this.appendPadding,
      pixelRatio: this.pixelRatio,
      animate: this.animate,
      limitInPlot: this.limitInPlot,
      plugins: ScrollBar
    })

    this.chart.source(this.data);

    for (let i = 0; i < this.geometry.length; i++) {
      if (this.geometry.size) {

        this.chart[this.geometry[i].type]()
          .position(
            this.geometry[i].position[0] + "*" + this.geometry[i].position[1]
          )
          .size(this.geometry[i].size)
          .color(this.geometry[i].color || "")
          .shape(this.geometry[i].shape || "")
          .adjust(this.geometry[i].adjust || false)
          .style(this.geometry[i].style || {})
          .animate(this.geometry[i].animation||true);
      } else {
        console.log('Type of animation: ' + this.geometry[i].animation)
        this.chart[this.geometry[i].type]()
          .position(
            this.geometry[i].position[0] + "*" + this.geometry[i].position[1]
          )
          .color(this.geometry[i].color || "")
          .shape(this.geometry[i].shape || "")
          .adjust(this.geometry[i].adjust || false)
          .style(this.geometry[i].style || {})
          .animate((this.geometry[i].animation||this.geometry[i].animation===false)?this.geometry[i].animation:true);
          /* .animate(this.geometry[i].animation||true); */
      }
    }

    if (this.scale) {
      this.scale.forEach((e, i) => {
        this.chart.scale(e.field, e.config);
      });
    }

    this.chart.coord(this.coord.type, this.coord.config);

    if (this.axis) {
      this.axis.forEach((e, i) => {
        this.chart.axis(e.field, e.config);
      });
    }

    //Setting Legend
    console.log('Legend is: ' + this.legend)
    if (Array.isArray(this.legend)&&this.legend.length>0) {
      this.legend.forEach((e,i)=> {
        this.chart.legend(this.legend[i].field, this.legend[i].config)
      })
    } else if (typeof this.legend === 'object') {
      this.chart.legend(this.legend.field, this.legend.config)
    } else if (this.legend === false) {
      this.chart.legend(false)
    }

    //Setting Tooltip
    if (this.tooltip) {
      this.chart.tooltip(this.tooltip)
    }

    
    //This settings is making tooltip appearing by mouseover on desktop
    /* this.chart.tooltip({
      triggerOn: [
        'touchstart', 
        'touchmove',
        'click',
        'mousemove'
      ]
    }) */

    //Setting Guide
    if (this.guide) {
      if (Array.isArray(this.guide)&&this.guide.length>0) {
        this.guide.forEach((e,i) => {
          this.chart.guide()[this.guide[i].type](this.guide[i].config)
        })
      } else if (typeof this.guide === 'object') {
        this.chart.guide()[this.guide.type](this.guide.config)
      }
    }

    //Setting ScrollBar
    if (this.scrollBar) {
      this.chart.scrollBar(this.scrollBar)
    }

    this.chart.render();
  },
  methods: {
    get(param) {
      return this.chart.get(param)
    }
  }
}
</script>