<script>
    export default {
        props: {
            changeInput: {
                type: Function,
                required: true
            },
            addTask: {
                type: Function,
                required: true
            }
        },
        data() {
            return {
                // Объекты переменные
            }
        }
    }
</script>

<template>
    <input type="text" @input="changeInput($event.target.value)">
    <button @click="addTask()">+</button>
</template>

<style scoped>
    input {
        width: 500px;
        position: relative;
        font-size: 1.2em;
        border-radius: 3px;
        border: 0;
        padding: 10px 15px;
        background: #fafafa;
        color: 333;
        outline: none;
    }

    button {
        position: relative;
        top: -2px;
        padding: 15px 20px;
        color: #fff;
        text-transform: uppercase;
        cursor: pointer;
        background: #0f4b1b;
        border: 0;
        border-radius: 3px;
    }

    button.fav-button {
        margin-left: 20px;
    }

    p {
        position: relative;
        top: -52px;
    }
</style>