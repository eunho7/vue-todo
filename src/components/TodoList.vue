<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" class="shadow">
            <i class="checkBtn fa-solid fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
                v-on:click="toggleComplete(todoItem, index)"></i>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
            <span class="removeBtn">
                <i class="fa-solid fa-trash-can" v-on:click="removeTodo(todoItem, index)"></i>
            </span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            todoItems: []
        }
    },
    methods: {
        removeTodo: function(todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        },
        toggleComplete(todoItem, index) {
            // console.log(todoItem, index);
            todoItem.completed = !todoItem.completed;
            // 로컬 스토리지 갱신
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        }
    },
    created: function () {
        if (localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++) {
                // console.log(JSON.parse(localStorage.getItem(localStorage.key(i))))
                // this.todoItems.push(localStorage.key(i));
                // console.log(localStorage.key(i));
                this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            }
        }
    }
}
</script>

<style scoped>
ul {
    /* 쩜 없애는거 */
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}

li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}

.removeBtn {
    margin-left: auto;
    color: #de4343;
}

.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}

.checkBtnCompleted {
    color: #b3adad;
}

.textCompleted {
    text-decoration: line-through;
    color: #b3adad;
}

/* 뷰 트랜지션 */
.list-item {
    display: inline-block;
    margin-right: 10px;
}

.list-enter-active,
.list-leave-active {
    transition: all 1s;
}

.list-enter,
.list-leave-to

/* .list-leave-active below version 2.1.8 */
    {
    opacity: 0;
    transform: translateY(30px);
}
</style>