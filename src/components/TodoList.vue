<template>
  <ul>
    <li v-for="(item, index) in list" v-bind:key="index">
      <!-- list에 중복된 값이 있을 경우가 있기 때문에 유니크한 키값을 넣어줌/ 아이디 값이 없기 때문에 인덱스 값을 만들어서 넣어준거 임 -->
      <span>{{ item }}</span>
      <button v-on:click="removeItem(item, index)">remove</button>
    </li>
  </ul>
</template>

<script>
import { bus } from '../utils/bus';

export default {
  // props: ['list'],
  props: {
    list: Array
  },
  // data() {
  //   return {
  //     todoItems: []
  //   };
  // },
  methods: {
    // fetchItems: function() {
    //   for (var i = 0; i < localStorage.length; i++) {
    //     var item = localStorage.key(i);
    //     this.todoItems.push(item);
    //   }
    // },
    removeItem: function(item, index) {
      // console.log("clicked", item, index);
      // 아래 두줄을 app뷰로
      // this.todoItems.splice(index, 1);
      // localStorage.removeItem(item);
      this.$emit('remove-todo', item, index)
    },
    removeItems: function() {
      this.todoItems = [];
    }
  },
  // created: function() {
  //   // console.log("created");
  //   // debugger
  //   this.fetchItems();
  // },
  beforeMount: function() {
    bus.$on('remove-all', this.removeItems);
    // console.log("before mount");
    // JSON.parse();
    // JSON.stringify();
    // window.addEventListener('scroll', function() {
    //   // ...
    // })
    // window.removeEventListener('scroll', )
  },
  beforeDestroy: function() {
    bus.$off('remove-all', this.removeItem);
  }
};
</script>

<style></style>
