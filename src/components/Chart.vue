<template>
  <div
    ref="chart"
    data-test="billboard-chart"
  />
</template>

<script lang="ts">
import { defineComponent, PropType, ref, computed, watch, nextTick } from 'vue';
import bb, { areaSpline } from 'billboard.js';

interface datasetItem {
  date: string,
  performance: number
}

export default defineComponent({
  props: {
    dataset: {
      type: Object as PropType<datasetItem[]>,
      required: true
    },
  },
  setup(props) {
    console.log(props)
    const chart = ref()
    const chartItem = ref()
    const chartData = computed(() => {
      return {
        json: props.dataset,
        keys: {
          x: 'date',
          value: ['performance'],
        },
        type: areaSpline(),
      };
    })

    const drawChart = () => {
      chartItem.value = bb.generate({
        data: chartData.value,
        axis: {
          x: {
            show: true,
            type: 'timeseries',
          },
        },
        bindto: chart.value,
      });
    }

    watch(chartData, () => {
      chartItem.value.load(chartData.value)
    })
    nextTick(drawChart)

    return {
      chart,
      chartItem
    }
  },
});
</script>
