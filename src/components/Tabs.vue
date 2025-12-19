<script>
    export default {

    }
</script>

<template>
    <button>Все</button>
    <button>Активные</button>
    <button>Завершённые</button>
</template>

<style scoped>
    button {
        height: 31px;
        background: none;
        width: 160px;
        font-size: 20px;
        margin: 5px;
        cursor: pointer;
        background: rgba(255, 255, 255, 0.474);
        border-radius: 10px;
        border: none;
        border: rgba(47, 52, 175, 0.421) solid 2px;
    }

    button:active {
        background: rgba(187, 187, 187, 0.474);
    }
</style>