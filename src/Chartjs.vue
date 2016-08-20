<template>
  <canvas class="chartjs" :width="width" :height="height"></canvas>
</template>

<script>
import Chart from 'chart.js' // With moment.js

const types = ['line', 'bar', 'radar', 'polarArea', 'pie', 'doughnut']

export default {

  props: {
    width: Number,
    height: Number,
    type: {
      type: String,
      required: true,
      validator (value) {
        return types.indexOf(value) > -1
      }
    },
    data: {
      type: Object,
      required: true,
      default () {
        return {}
      }
    },
    options: {
      type: Object,
      default () {
        return {}
      }
    }
  },

  mounted () {
    const $el = this.$el
    this.chart = new Chart($el, {
      type: this.type,
      data: this.data,
      options: this.options
    })
  },

  data () {
    return {
      chart: null
    }
  },

  watch: {
    data (val) {
      this.$nextTick(() => {
        // this.chart.data.datasets = val.datasets
        // this.chart.data.labels = val.labels
        this.chart.update()
      })
    }
  }
}
</script>

<style lang="scss">
canvas.chartjs {
  max-width: 100%;
}
</style>
