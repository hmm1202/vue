<template>
  <div id="app">
    <h1>我的博客</h1>
    <comment-form @add-comment="doAdd" />
    <comment-list title="热门评论" :comments="comments" @delete-comment="doDelete" />
  </div>
</template>

<script>
 import CommentForm from './components/comment-form.vue';
 import CommentList from './components/comment-list.vue';

 export default {
   name: 'App',
   data() {
     return  {
       comments: [
         { author: "张三", body: "今天是个好日子" },
         { author: "王五", body: "上课睡觉真舒服" }
       ]
     }
   },
   methods: {
     doDelete(b) {
       this.comments = this.comments.filter((e) => e.body != b);
     },
     doAdd(comment) {
       this.comments.push(comment);
     }
   },
   components: {
     CommentForm, CommentList
   }
 }
</script>

<style>
 #app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   text-align: center;
   color: #2c3e50;
   margin-top: 60px;
 }
</style>