<template>
    <div class="flex flex-col bg-white w-full h-full rounded-lg overflow-hidden">
        <home-tool-box-tab />
        <home-tool-box-content>
            <div class="flex flex-col gap-10">
                <div class="flex items-center justify-center w-32 h-32 rounded-full bg-yellow-500">
                    <text-base font-size="text-6xl" font-color="text-white">!</text-base>
                </div>
                <text-base>Deposit Required</text-base>
            </div>
        </home-tool-box-content>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import TextBase from "@/components/Base/Text/TextBase.vue";
import HomeToolBoxTab from "@/components/Page/Home/HomeToolBoxTab.vue";
import HomeToolBoxContent from "@/components/Page/Home/HomeToolBoxContent.vue";

export default defineComponent({
    components: {
        HomeToolBoxTab,
        HomeToolBoxContent,
        TextBase
    }
})
</script>