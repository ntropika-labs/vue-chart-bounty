<template>
  <div ref="chart" data-test="billboard-chart"></div>
</template>

<script>
import bb, { areaSpline } from 'billboard.js';

const isDatasetItem = (item) => typeof item === 'object'
    && typeof item.date === 'string'
    && typeof item.performance === 'number';
const validDataset = (dataset) => dataset.every(isDatasetItem);

export default {
  props: {
    dataset: {
      type: Array,
      required: true,
      validator(dataset) {
        return Array.isArray(dataset) && validDataset(dataset);
      },
    },
  },
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    chartData: {
      deep: true,
      handler() {
        this.updateChart();
      },
    },
  },
  computed: {
    chartData() {
      return {
        json: this.dataset,
        keys: {
          x: 'date',
          value: ['performance'],
        },
        type: areaSpline(),
      };
    },
  },
  mounted() {
    this.$nextTick(this.drawChart);
  },
  methods: {
    drawChart() {
      this.chart = bb.generate({
        data: this.chartData,
        axis: {
          x: {
            show: true,
            type: 'timeseries',
          },
        },
        bindto: this.$refs.chart,
      });
    },
    updateChart() {
      this.chart.load(this.chartData);
    },
  },
};
</script>
