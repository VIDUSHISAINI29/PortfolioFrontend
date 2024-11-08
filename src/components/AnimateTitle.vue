<script>
import { onMounted } from 'vue';
import * as echarts from 'echarts';

export default {
  name: 'AnimationChart',
  setup() {
    const initializeChart = () => {
      const chartDom = document.getElementById('chart');
      const myChart = echarts.init(chartDom);

      const option = {
        graphic: {
          elements: [
            {
              type: 'text',
              left: 'center',
              top: 'center',
              style: {
                text: 'Fullstack Web Developers',
                fontSize: 40,
                fontWeight: 'bold',
                lineDash: [0, 200],
                lineDashOffset: 0,
                fill: '#e38007',
                stroke: '#e75334',
                lineWidth: 1,
              },
              keyframeAnimation: {
                duration: 4000, // Animation duration
                loop: true,
                keyframes: [
                  {
                    percent: 0.7,
                    style: {
                      fill: 'transparent',
                      lineDashOffset: 200,
                      lineDash: [200, 0],
                    },
                  },
                  {
                    percent: 0.8,
                    style: {
                      fill: 'transparent',
                    },
                  },
                  {
                    percent: 1,
                    style: {
                      fill: '#FF7F50',
                    },
                  },
                ],
              },
            },
          ],
        },
      };

      // Set options and add a delay for loop
      myChart.setOption(option);

      // Delay restart of animation by 2 seconds
      setTimeout(() => {
        myChart.clear(); // Clear the chart to reset the animation
        initializeChart(); // Restart the chart with the same options
      }, 8000); // Total loop duration (4s animation + 2s pause)
    };

    onMounted(() => {
      initializeChart();
    });
  },
};
</script>

<template>
  <span id="chart" class="tw-w-[500px] tw-hidden md:tw-flex  tw-h-[70px] tw-rounded-lg tw-text-start" ></span>
</template>
