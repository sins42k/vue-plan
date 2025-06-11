<script >
  import TodoHeader from './components/TodoHeader.vue';
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';

  export default{
    components: {
      TodoHeader,
      TodoInput,
      TodoList,
    },
    data(){
      return {
        todo: [], // 1
        current: 'all',
      }
    },
    computed:{
      computedTodo(){
        if(this.current === 'all'){
          return this.todo;
        } else {
          return this.todo.filter((v)=>v.completed);
        };
      },
    },
    methods: {
      addTodo(inputMsg){      // 2
        const item ={         // 3
          id: Math.random(),  // 고유한 값
          msg: inputMsg,      // 할 일 텍스트
          completed: false,   // 할 일 완료 여부
        };
        this.todo.push(item); // 4
        },
      updateTab(tab) {
        this.current = tab;
      },
      deleteTodo(id) {
        this.todo = this.todo.filter((v)=> v.id !== id);
      },
      updateTodo(id) {
        this.todo = this.todo.map((v) =>
          v.id === id? {...v, completed: !v.completed} :v
          );
      },
    },
  }
  
</script>

<template>
  <div class="todo">
    <TodoHeader :current="current" @update-tab="updateTab"/> 
    <!-- TodoList 컴포넌트로 computedTodo 데이터 전달-->
    <TodoList 
      :computed-todo="computedTodo"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"/> 
    <TodoInput @add-todo="addTodo"/> 
  </div>
</template>

<style >
</style>