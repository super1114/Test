<template>
  <div :class="['relative bg-white rounded-lg transition', loading ? '' : '']">
    <!-- loading -->
    <base-loading v-if="loading" />
    <div class="flex justify-between pt-10 px-10">
        <!-- price -->
        <div class="flex gap-5">
            <div class="flex items-center">
                <i class="fa-regular fa-dollar-sign text-xl" />
                <text-base font-size="text-4xl">
                    {{ Intl.NumberFormat().format(currentPrice) }}
                </text-base>
                <text-base font-size="text-xl">
                    .{{ currentPricePrecision }}
                </text-base>
            </div>

            <div class="flex flex-col items-start">
                <text-base font-size="text-lg" :font-color="[precent < 0 ? 'text-rose-500' : 'text-green-500'].toString()">{{ precent >= 0 ? '+' + precent + '%' : precent + '%' }}</text-base>
            </div>
        </div>

        <!-- time frame -->
        <home-line-chart-time-frame-wrapper>
            <home-line-chart-time-frame-item v-for="timeframe in timeframes" :key="timeframe.label" @click="changeTimeframe(timeframe.id)">
                <text-base v-if="currentTimeframe === timeframe.id" font-color="text-orange-600" font-size="text-sm">{{ timeframe.label }}</text-base>
                <text-base v-else font-color="text-gray-500" font-size="text-sm">{{ timeframe.label }}</text-base>
            </home-line-chart-time-frame-item>
        </home-line-chart-time-frame-wrapper>
    </div>
    <apex-chart
      type="area"
      height="380"
      :options="chartOptions"
      :series="series"
    ></apex-chart>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import VueApexCharts from "vue3-apexcharts";
import axios from 'axios';

import HomeLineChartTimeFrameWrapper from "@/components/Page/Home/HomeLineChartTimeFrameWrapper.vue"
import HomeLineChartTimeFrameItem from "@/components/Page/Home/HomeLineChartTimeFrameItem.vue"
import TextBase from "@/components/Base/Text/TextBase.vue";
import BaseLoading from "@/components/Base/BaseLoading.vue"

let interval: number;

export default defineComponent({
    data() {
        return {
            chartOptions: {
                chart: {
                    type: 'area',
                    stacked: false,
                    height: 350,
                    zoom: {
                        enabled: false
                    },
                    toolbar: {
                        show: false
                    }
                },
                colors: ['#ea580c'],
                stroke: {
                    width: 1
                },
                dataLabels: {
                    enabled: false
                },
                markers: {
                    size: 0,
                },
                fill: {
                    type: 'gradient',
                    gradient: {
                        shadeIntensity: 1,
                        inverseColors: false,
                        opacityFrom: 0,
                        opacityTo: 0,
                        stops: [20, 100, 100, 100]
                    },
                },
                yaxis: {
                    show: false
                },
                xaxis: {
                    type: 'datetime',
                },
                tooltip: {
                    shared: true
                },
                grid: {
                    yaxis: {
                        lines: {
                            show: false
                        }
                    }
                }
            },
            series: [
                {
                    name: "BTC",
                    data: [],
                },
            ],
            timeframes: [
                {
                    id: 0,
                    label: '1H',
                    time: -Infinity
                },
                {
                    id: 1,
                    label: '1D',
                    time: 1
                },
                {
                    id: 2,
                    label: '1W',
                    time: 7
                },
                {
                    id: 3,
                    label: '1M',
                    time: 31
                },
                {
                    id: 4,
                    label: '1Y',
                    time: 365
                },
                {
                    id: 5,
                    label: 'All',
                    time: Infinity
                }
            ],
            currentPrice: 0,
            currentPricePrecision: 0,
            precent: 0,
            currentTimeframe: 0,
            loading: false
        };
    },
    components: {
        apexChart: VueApexCharts,
        TextBase,
        HomeLineChartTimeFrameWrapper,
        HomeLineChartTimeFrameItem,
        BaseLoading
    },
    methods: {
        async getData() {
            this.loading = true;

            let date = new Date();
            let to = Math.floor(date.getTime() / 1000);
            let from = 0;
            if(this.currentTimeframe === 0) {
                from = to - 3600;
            } else if(this.currentTimeframe === 5) {
                date = new Date(1970, 0, 1);
                from = Math.floor(date.getTime() / 1000);
            } else {
                date.setDate(date.getDate() - this.timeframes[this.currentTimeframe].time);
                from = Math.floor(date.getTime() / 1000);
            }
            const res = await axios.get(`https://api.coingecko.com/api/v3/coins/bitcoin/market_chart/range?vs_currency=usd&from=${from}&to=${to}`);
            this.series[0].data = res.data.prices;
            this.currentPrice = Math.floor(res.data.prices[res.data.prices.length - 1][1]);
            this.currentPricePrecision = Math.floor(parseFloat(((res.data.prices[res.data.prices.length - 1][1] - this.currentPrice) * 100).toFixed(2)))
            this.precent = parseFloat(((res.data.prices[res.data.prices.length - 1][1] - res.data.prices[0][1]) / 100).toFixed(2));

            this.loading = false;
        },
        changeTimeframe(timeframe: number) {
            this.currentTimeframe = timeframe;
        }
    },
    mounted() {
        this.getData();
        
        interval = setInterval(() => {
            this.getData();
        }, 60000)
    },
    unmounted() {
        clearInterval(interval);
    },
    watch: {
        currentTimeframe(newTimeframe, oldTimeframe) {
            this.getData();
        }
    }
})
</script>
