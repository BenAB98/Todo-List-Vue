<script setup>
defineProps(["todo"]);
defineEmits(["delete","complete"]);
</script>

<template>
    <div :class="['todo',{checked:todo.isDone}]">
        <p class="todo-title">{{todo.title}}</p>
        <span class="created-at">{{ new Date(todo.createdAt).toLocaleDateString('zh-Hans-CN') }}</span>
        <input class="checkbox" type="checkbox" :checked="todo.isDone" @change="$emit('complete')"/>
        <button @click="$emit('delete')">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" width="25" stroke-width="1.5" stroke="currentColor" class="trash">
            <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
            </svg>
        </button>
    </div>
</template>

<style scoped>
.todo{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: var(--secondaryColor);
    margin: .3rem 0;
    transition: all .2s ease;
    border-radius: 8px;
    overflow: hidden;
}

.todo p{
    flex: 1;
    color: var(--primaryColor);
    font-weight: bold;
}

.todo button{
    border: none;
    outline: none;
    cursor: pointer;
    padding: .5rem;
}

.todo span svg{
    cursor: pointer;
}

.todo-title{
    padding-left: .5rem;
}

.trash{
    color: var(--mainRed);
}

.check{
    color: var(--primaryColor);
}
.checked{
    text-decoration: line-through;
    opacity: .4;
}

.checkbox {
  margin: 0px 4px 4px 0;
  width: 20px;
  height: 20px;
}

.created-at{
    color: var(--primaryColor);
    margin-right: .75rem;
}
</style>