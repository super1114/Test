<template>
    <div class="w-full grid grid-cols-3 divide-x">
        <home-tool-box-tab-item v-for="tab in tabs" :key="tab.id" :active="tab.id === currentTab" @click="changeTab(tab.id)">
            {{ tab.label }}
        </home-tool-box-tab-item>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import HomeToolBoxTabItem from '@/components/Page/Home/HomeToolBoxTabItem.vue'

export default defineComponent({
    data() {
        return {
            tabs: [
                {
                    id: 0,
                    label: 'Buy'
                },
                {
                    id: 1,
                    label: 'Sell'
                },
                {
                    id: 2,
                    label: 'Convert'
                }
            ],
            currentTab: 0
        }
    },
    methods: {
        changeTab(tab: number) {
            this.currentTab = tab;
        }
    },
    components: {
        HomeToolBoxTabItem
    }
})
</script>