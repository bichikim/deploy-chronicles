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
})
</script>

<template>
    <QrcodeVue :value="value" :size="size" :image-settings="{width: 50, height: 50, src: '/images/wavve.png', excavate: true}" />
</template>
