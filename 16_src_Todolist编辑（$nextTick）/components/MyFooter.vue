<template>
    <!-- 隐形类型转换 -->
    <div class="todo-footer" v-show="total">
        <label>
            <!-- 这里也可以用v-model来替代，此时不需要计算属性了  -->
             <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
            <input type="checkbox" v-model="isAll"/>
        </label> 
        <span>
            <span>已完成{{doneTotal}}</span> /全部{{ total }}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div> 
</template>

<script>
export default{
    name:"MyFooter",
    props:['todos'],
    computed:{
        total(){
            return this.todos.length;
        },
        doneTotal(){
            return this.todos.reduce((todoTotal,todo) => {
                return todoTotal + todo.done;
            },0);
            //return this.todos.filter(todo => todo.done).length;
        },
        isAll:{
            get(){
                return this.total === this.doneTotal && this.doneTotal > 0;//计算属性可以通过其他的计算属性接着进行计算的到结果
            },
            set(value){
                //value注意要么为ture，要么为false，因为你是把它应用在看checkbox上
                //this.checkAllTodo(value);
                //采用自定义事件来修改
                this.$emit('checkAllTodo',value);
            }
        }
    },
    methods:{
        //checkAll(e){
        //consle.log(e.target.checked);//判断这个checkbox到底是不是全选ture全选false全不选
        //this.checkAlltodo(e.target.checked);
        //}
        clearAll(){
            //this.clearAllDone();
            //修改为自定事件
            this.$emit('clearAllDoneTodo');
        }
    }
}
</script>

<style scoped>
.todo-footer{
    height: 40px;
    line-height: 40px;
    padding-left: 20px;
    cursor: pointer;
}

.todo-footer label input{
    position: relative;
    top:-1px;
    vertical-align: middle;
    margin-right: 5px;
}

.todo-footer button{
    float: right;
    margin-top: 5px;
}
</style>