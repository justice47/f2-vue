<template>
  <div>
    <canvas id="mountNode"></canvas>
  </div>
</template>

<script>
import F2 from "@antv/f2";

export default {
  name: "f2chart",
  props: {
    data: {
      type: Array,
      required: true
    },
    geometry: {
      required: true
    },
  },
  data() {
    return {};
  },
  mounted() {
    const chart = new F2.Chart({
      id: "mountNode",
    })
    chart.source(this.data);
    for (let i = 0; i < this.geometry.length; i++) {
      chart[this.geometry[i].type]()
        .position(
          this.geometry[i].position[0] + "*" + this.geometry[i].position[1]
        )
    }

    chart.render();
  }
}
</script>