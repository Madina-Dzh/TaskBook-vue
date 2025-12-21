<script>
    export default {
        props: {
            text: {
                type: String,
                required: true
            },
            deleteTask: {
                type: Function,
                required: true
            },
            setStatus: {
                type: Function,
                required: true
            },
            selectTask: {
                type: Number,
                required: true
            },
            id: {
                type: String,
                required: true
            },
            status: {
                type: Boolean,
                required: true
            }
        },
        data() {
            return {
                completed: false
            }
        },
        methods: {
            markAsCompleted() {
                //console.log(this.index)
                //console.log(this.completed)
                //this.completed = !this.completed;
                //this.setStatus(this.index, this.completed);
                this.completed = !this.status
                this.setStatus(this.id, !this.status);
            }
        },
        mounted() {
            this.completed = this.status;
        },
        watch: {
            status(newVal) {
                this.completed = newVal;
            }
        }
    }
</script>

<template>
    <div class="task" :class="{task: true, completed: completed}">
        {{text}}
        <div>
            <button v-if="completed == false" @click="markAsCompleted()"
                style="background-color: #40ff006c;">&#10004;</button>
            <button v-else @click="markAsCompleted()" style="background-color: rgba(64, 255, 0, 0.425);">X</button>
            <button @click="deleteTask(id)" style="background-color: rgba(255, 0, 0, 0.425);">&#9249;</button>
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
        cursor: pointer;
        border-radius: 10px;
        border: none;
        border: rgba(47, 52, 175, 0.421) solid 2px;
    }

    .task.completed {
        background-color: rgba(255, 185, 192, 0.355);
        text-decoration: line-through;
    }

    .task.completed span {
        text-decoration: line-through;
    }

    .task:hover {
        transform: scale(1.05);
        transition: transform(0.2s);
    }
</style>