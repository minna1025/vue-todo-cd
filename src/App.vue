<template>
  <!-- HTML -->
  <div>
    <todo-header></todo-header>
    <todo-input v-on:add-todo="addTodoItem"></todo-input>
    <!-- <todo-list v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></todo-list> -->
    <todo-list v-bind:list="todoItems" v-on:remove-todo="removeTodoItem"></todo-list>
    <!-- <todo-footer v-on:clear="clearAllItems"></todo-footer> -->
    <todo-footer v-on:remove-all="clearAllItems"></todo-footer>
  </div>
</template>

<script>
// 컴포넌트 로딩 단축키 이름 'vim'
// import 컴포넌트 이름 from '파일 경로'
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "@/components/TodoInput.vue";
import TodoList from "@/components/TodoList.vue";
import TodoFooter from "@/components/TodoFooter.vue";

// var TodoHeader = {
//   template: '<h1>Todo App</h1>'
// }

export default {
  // Javascript
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  },
  data() {
    return {
      todoItems: []
    };
  },
  methods: {
    fetchItems: function() {
      // 투두아이템에 가지고 잇는 정보를 넣어줌
      for (var i = 0; i < localStorage.length; i++) {
        var item = localStorage.key(i);
        this.todoItems.push(item);
      }
    },
    addTodoItem: function(value) {
      // 뷰 데이터 목록에 값 추가
      this.todoItems.push(value);
      // 디비에 값 저장
      localStorage.setItem(value, value);
    },
    removeTodoItem: function(item, index) {
      this.todoItems.splice(index, 1);
      localStorage.removeItem(item);
    },
    clearAllItems: function() {
      // 뷰 데이터 목록 초기화
      this.todoItems = [];
      // DB(브라우저 저장소) 초기화
      localStorage.clear();
    }
  },
  created() {
    // 메소드에 들어가도 오류가 안남 개선됏음 좋겟다리
    // 제일 처음 시작됨
    this.fetchItems();
  }
};
// 인스턴스 옵션에는 어로우펑션을 못씀
// vm인 this 땜시 그래서 어로우 펑션으로 만 쓰는게 아니라
// created: function (){} => created(){}

// for (value in arr){
//   console.log(value)
// }

// new Vue({
//   components: {

//   }
// })
</script>

<style>
/* CSS */
</style>
