<template>
    <div :class="['flex items-center justify-center h-16 border-y cursor-pointer transition', active ? 'text-blue-600 border-b-transparent border-t-blue-600' : '']">
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