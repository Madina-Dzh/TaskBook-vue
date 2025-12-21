<script>
    export default {
        props: {
            selectTask: {
                type: Number,
                required: true
            },
            selectStatus: {
                type: Function,
                required: true
            }
        },
        methods: {
            isSelected(index) {
                return this.selectTask === index;
            }
        }
    }
</script>

<template>
    <div>
        <button v-for="(item, index) in ['Все', 'Активные', 'Завершённые']" :key="index"
            :class="{ selected: isSelected(index) }" @click="selectStatus(index)">
            {{ item }}
        </button>
    </div>
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

    .selected {
        background-color: #DCDCDC !important;
    }

    button:active {
        background: rgba(187, 187, 187, 0.474);
    }
</style>