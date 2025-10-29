<script setup lang="ts">
import QrcodeVue from 'qrcode.vue'

defineProps({
    value: {
        type: String,
        required: true,
    },
    size: {
        type: Number,
        default: 100,
    },
    level: {
        type: String,
        default: 'L',
    },
    labelSize: {
        type: Number,
        default: 50,
    },
})
</script>

<template>
    <QrcodeVue :value="value" :size="size" :image-settings="{width: labelSize, height: labelSize, src: '/images/wavve.png', excavate: true}" />
</template>
