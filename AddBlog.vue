<template>
 <div class="add-blog">
   <h2>添加博客</h2>
   <form v-if="!submmited">
       <lable>博客标题</lable>
       <input type="text" v-model="blog.title" required/>
      <lable>博客内容</lable> 
      <textarea v-model="blog.content"></textarea>
      <div id="checkbox">
          <label>Vue.js</label>
          <input type="checkbox" value="Vue.js" v-model="blog.categories">
             <label>Node.js</label>
          <input type="checkbox" value="Node.js" v-model="blog.categories">
             <label>React.js</label>
          <input type="checkbox" value="React.js" v-model="blog.categories">
             <label>Angular</label>
          <input type="checkbox" value="Angular" v-model="blog.categories">
      </div>
      <label>作者</label>
      <select v-model="blog.author">
      <option v-for="author in authors" :key="author">
          
          {{author}}
          </option>  

      </select>
      <button v-on:click.prevent="post">添加博客</button>
   </form>
   <div v-if="submmited">
     <h3>您的博客发布成功</h3>
    </div>
   <div id="preview">
       <h3>博客总览</h3>
       <p>博客标题：{{blog.title}}</p>
        <p>博客内容：</p>
        <p>{{blog.content}}</p>
        <p>博客分类：</p>
        <ul>
            <li 
            v-for="category in blog.categories"
            :key="category"
            >{{category}}
            </li>
        </ul>
       <p>作者：{{blog.author}}</p>


   </div>
  </div>
</template>

<script>

export default {
  name: 'App',
    data(){
      return {
         blog:{
          title:"",
               content:"",
              categories:[],
              author:''
       },
           authors:["Hemiah","Henry","bucky"],
          submmited:false
      }
  },
  methods:{
      post:function(){
          this.$http.post("http://jsonplaceholder.typicode.com/posts/",{
              title:this.blog.title,
              body:this.blog.content,
              userId:3
          })
          .then(function(data){
              console.log(data);
              this.submmited=true;
          })
      }
  }
  
       
   

  
}
</script>

<style>
#add-blog{
    box-sizing:border-box;
}
#add-blog{
    margin:20px auto;
    max-width:600px;
    padding:20px;
} 
lable{
    display:block;
    margin:20px 0 10px;
}
input[type="text"],textarea,select{
display:block;
width:100%;
padding:8px;
}
textarea{
    height:200px;
}
#checkbox lable{
 display:inline-block;
 margin-top:0;
}
#checkbox input{
 display:inline-block;
 margin-right:10px;
}
button{
    display:block;
    margin:20px 0;
    background:crimson;
    color:#fff;
    border:0;
    padding:14px;
    border-radius:4px;
    font-size:18px;
    cursor:pointer;
}
#preview{
    padding:10px 20px;
    border:1px dotted #ccc;
    margin:30px 0;
}
h3{
    margin-top:10px;
}
</style>
