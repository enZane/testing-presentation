<script setup>
defineProps({
    button: {
        type: String,
        required: true
    },
    operator: {
        type: Boolean,
        default: false
    }
})
</script>

<template>
    <button
        class="rounded-md bg-gray-100 h-10 w-full text-center text-lg"
        :bg="operator ? 'gray-200' : 'gray-100'"
        hover="border-3 border-purple-400"
        @click="$emit('input', button)"
    >{{ button }}</button>
</template>