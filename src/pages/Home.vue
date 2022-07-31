<template>
    <home-wrapper>
        <template #header>
            <home-header-wrapper>
                <template #left>
                    <div class="flex items-center gap-5">
                        <img src="https://s2.coinmarketcap.com/static/img/coins/64x64/1.png" class="w-10 h-10" alt="btc" />
                        <div class="flex items-baseline gap-3">
                            <text-base font-weight="font-bold" font-size="text-3xl">Bitcoin</text-base>
                            <text-base font-weight="font-bold" font-size="text-2xl" font-color="text-gray-500">BTC</text-base>
                        </div>
                    </div>
                </template>

                <template #right>
                    <button-square>
                        <i class="fa-solid fa-star mr-2 text-yellow-500"/>
                        <text-base font-weight="font-medium">Watchlist</text-base>
                    </button-square>
                </template>
            </home-header-wrapper>

            <home-content-wrapper>
                <template #tab>
                    <home-tab-menu />
                </template>

                <template #body>
                    <home-body-wrapper>
                        <div class="col-span-2">
                            <home-line-chart />
                        </div>
                        
                        <div class="col-span-1">
                            <home-tool-box />
                        </div>
                    </home-body-wrapper>
                </template>
            </home-content-wrapper>
        </template>
    </home-wrapper>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import HomeWrapper from "@/components/Page/Home/HomeWrapper.vue";
import HomeHeaderWrapper from "@/components/Page/Home/HomeHeaderWrapper.vue";
import HomeContentWrapper from "@/components/Page/Home/HomeContentWrapper.vue";
import HomeBodyWrapper from "@/components/Page/Home/HomeBodyWrapper.vue";
import HomeTabMenu from "@/components/Page/Home/HomeTabMenu.vue";
import HomeLineChart from "@/components/Page/Home/HomeLineChart.vue";
import HomeToolBox from "@/components/Page/Home/HomeToolBox.vue";
import TextBase from "@/components/Base/Text/TextBase.vue";
import ButtonSquare from "@/components/Base/Button/ButtonSquare.vue";

export default defineComponent({
    components: {
        HomeWrapper,
        HomeHeaderWrapper,
        HomeContentWrapper,
        HomeBodyWrapper,
        HomeTabMenu,
        HomeLineChart,
        HomeToolBox,
        TextBase,
        ButtonSquare
    }
})
</script>