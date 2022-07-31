<template>
    <div :class="['flex items-center h-10 px-10 rounded-full cursor-pointer transition', active ? 'bg-blue-600 text-white' : ' bg-gray-100 hover:bg-gray-200 text-black']">
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