<template>
    <div :class="['flex items-center justify-center h-16 px-1 mt-[0.5px] text-gray-500 cursor-pointer transition', active ? 'text-black font-bold border-b-2 border-b-black' : '']">
        <slot />
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    props: {
        active: {
            type: Boolean,
            required: false,
            default: false
        }
    }
})
</script>