<template>
    <span :class="[fontWeight, fontSize, fontColor]">
        <slot />
    </span>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    props: {
        fontWeight: {
            type: String,
            required: false,
            default: "font-normal"
        },
        fontSize: {
            type: String,
            required: false,
            default: "text-base"
        },
        fontColor: {
            type: String,
            required: false,
            default: ""
        }
    }
})
</script>