<template>
    <div class="todo">
        <p class="header-title" @click="setSaying()">
            <span>{{ newSaying }}</span>
        </p>
        <p class="header-day">
            {{ today }}
        </p>
        <div class="input-box">
            <input type="text" v-model="newTodo" v-on:keyup.enter="addTodo">
        </div>
        <p class="title-desc">{{todos.length}}개가 남다.</p>
        <ul>
            <Card v-for="todo in todos" :key="todo.id" :todo="todo" @delete="removeTodo" @change="changeTodo" />
        </ul>
    </div>
</template>

<script>
import Card from '../components/Card'
import { onMounted } from 'vue'
import { getDate } from '../utils'
import useTodos from '../hooks/useTodos'
import useSaying from '../hooks/useSaying'

export default {
    name: 'Todo',
    components: {
        Card
    },
    setup() {
        const {
            todos,
            addTodo,
            removeTodo,
            newTodo,
            changeTodo
        } = useTodos()
        
        const {
            setSaying,
            newSaying
        } = useSaying()

        onMounted(() => {
            setSaying()
        })

        const today = getDate();
        return {
            todos,
            addTodo,
            removeTodo,
            newTodo,
            setSaying,
            newSaying,
            today,
            changeTodo
        }
    }
};
</script>

<style>
.header-title {
    text-align: center;
    height: 200px;
}

.header-title:hover {
    cursor: pointer;
}

.hedaer-title span {
    background-position-y: 0;
    background-image: linear-gradient(white 50%, gold 50%);
    transition: background .5s ease;
    background-size: 2px;
    background-size: auto 175%;
}

.hedaer-title span:hover {
    background-position-y: 100%;
}

.header-day {
    text-align: center;
    color: #eb596e;
}

.placeholder {
    width: 100%;
    height: 80px;
    background: #aaa;
    border-radius: 10px;
}

.title-desc {
    color: #aaa;
    text-align: right;
}

.todo {
    width: 500px;
    margin: 0 auto;
}

.input-box {
    position: relative;
    display: flex;
    transition: background .3s cubic-bezier(.25, .8, .5, 1);
    margin-bottom: 8px;
    min-height: inherit;
}

.input-box > input {
    flex: 1 1 auto;
    width: 100%;
    max-width: 100%;
    min-width: 0;
    max-height: 32px;
    line-height: 20px;
    background-color: transparent;
    border-style: none;
    font-family: "nanumburi";
}

.input-box > input:focus {
    outline: none;
}

.input-box::before {
    content: '';
    position: absolute;
    left: -0;
    bottom: -1px;
    width: 100%;
    transition: .3s cubic-bezier(.25, .8, .5, 1);
    -webkit-transition: .3s cubic-bezier(.25, .8, .5, 1);
    border-style: solid;
    border-width: thin 0 0;
    border-color: rgba(0,0,0, .42);
}

.input-box:focus, .input-box::before {
    border-color: red;
}

li > span {
    vertical-align: middle;
    display: inline-block;
}

li > span > input {
    position: relative;
    top: 1.3px;
}

ul {
    padding: 0;
    margin: 0 auto;
}

li {
    list-style: none;
    padding: 10px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
    margin-bottom: 20px;
    transition: all 0.3s cubic-bezier(.25, .8, .25, 1);
}

li:hover {
    box-shadow: 0 14px 28px rgba(0, 0, 0, .25), 0 10px 10px rgba(0, 0, 0, 0.22);
}

.desc {
    float: right;
    position: relative;
    top: 0;
    color: #eb596e;
}

.desc:hover,
.checkbox:hover {
    cursor: pointer;
}

</style>