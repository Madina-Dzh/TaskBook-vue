<script>
    export default {
        data() {
            return {
            }
        }
    }
</script>

<template>
    <div class="task">
        Текст задачи
        <div>
            <button style="background-color: rgba(229, 255, 0, 0.399);">&#9998;</button>
            <button style="background-color: rgba(255, 0, 0, 0.425);">&#9249;</button>
        </div>

    </div>
</template>

<style scoped>
    .task {
        margin: auto;
        padding: auto;
        background: rgba(255, 185, 192, 0.668);
        border-radius: 30px;
        margin-bottom: 30px;
        padding: 0 20px;
        width: 850px;
        min-height: 60px;
        text-align: left;
        font-size: 20px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    button {
        height: 31px;
        background: none;
        width: 60px;
        font-size: 20px;
        margin-left: 5px;
        border-radius: 10px;
        border: none;
        border: rgba(47, 52, 175, 0.421) solid 2px;
    }
</style>