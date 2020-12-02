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
 import axios from 'axios';
 export default {
   name:"App",
   data() {
     return  {
       comments: [ ],
       author:"",
       body:""
     }
   },
   methods: {
     doDelete(id) {
       axios({
         url:"http://localhost:8088/Vue_war_exploded/task/del?id="+id,
         method:"post",
         responseType:"json"
       })
       this.loadcomment();
     },
     doAdd(data) {
              var rsp = new URLSearchParams();
              rsp.append("author",data.author);
              rsp.append("body",data.body);
              alert(rsp);
       axios({
         url:"http://localhost:8088/Vue_war_exploded/task/add",
         method:"post",
         responseType:"json",
         data:rsp,
       }).then(resp =>{
         this.author = "";
         this.body = "";
        this.loadcomment();
       })
        
     },
     loadcomment(){
        axios({
       url:"http://localhost:8088/Vue_war_exploded/tasks",
       responseType:"json"
     }).then(data =>{
       this.comments = data.data;
     })
     }
   },
   components: {
     CommentForm, CommentList
   },
   created(){
    this.loadcomment();
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
