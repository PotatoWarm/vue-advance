<template>
    <ul class="todo-main">
        <Iterm 
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"/>
    </ul>
</template>
<!-- 
    使用v-for指令遍历todos数组，
    将每个todo对象传递给Iterm组件
-->
<script>
import Iterm from '@/components/Iterm.vue';
export default {
    name: 'List',
    components: {
        Iterm,  
    },
    props: ['todos']
}
</script>

<style scoped>
.todo-main{
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
}

.todo-empty{
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
}
</style>
