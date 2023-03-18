<script setup>
import { ref, reactive } from 'vue'

let state = reactive({ count: 0})

const increment = () => {
    state = {
        count: state.count++
    }
}

</script>
<template>
    <h1>
        {{ state.count }}
    </h1>
    <button @click="increment">
        +
    </button>
</template>