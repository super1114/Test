<template>
    <home-tab-menu-wrapper>
        <home-tab-menu-item v-for="tab in tabs" :active="tab.id === currentTab" :key="tab.label" @click="changeTab(tab.id)">
            {{ tab.label }}
        </home-tab-menu-item>
    </home-tab-menu-wrapper>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import HomeTabMenuWrapper from "./HomeTabMenuWrapper.vue";
import HomeTabMenuItem from "./HomeTabMenuItem.vue";

export default defineComponent({
    data() {
        return {
            tabs: [
                {
                    id: 0,
                    label: "Overview"
                },
                {
                    id: 1,
                    label: "Wallet"
                },
                {
                    id: 2,
                    label: "Vault"
                },
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
        HomeTabMenuWrapper,
        HomeTabMenuItem
    }
})
</script>