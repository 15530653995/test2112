<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button v-bind:style="s" v-on:click = "changeCount()">{{count}}</button>
    <p>{{count.toFixed(2)}}</p>
    <p>{{str.toLowerCase()}}</p>
    <!-- 插值表达式不能应用在设置属性上 -->
    <p v-bind:class="red">{{str.toLocaleUpperCase()}}</p>
    <ul v-html = "li"></ul>
    <div>
      <input type="radio" :checked="danger==1" @click="danger=1">男
      <input type="radio" :checked="danger==0" @click="danger=0">女
    </div>
    <div>
      <div v-if="danger==1">男</div>
      <div v-if="danger==0">女</div>
    </div>
    <!-- 考试成绩评定 -->
    <div>考试成绩为{{ cj }}</div>
    <div>
      <span v-if="cj>90">评定A</span>
      <span v-else-if="cj>80">评定B</span>
      <span v-else-if="cj>70">评定C</span>
      <span v-else>评定D</span>
    </div>
    <div>
      <span v-for="(str,i) in pf" :key="i">{{str}}</span>
    </div>
    <h1>点击按钮换图</h1>
    <h2>
      <button @click="changeImg('-')">上一页</button>
      <span>{{ rotation[rotationIndex].name }}</span>
      <button @click="changeImg('+')">下一页</button>
    </h2>
    <div v-show="isAlert">图片到头了</div>
  </div>
</template>


<script>
export default {
  name: 'HelloWorld',
  // 当前页面是组件页面，项目是通过vue create 项目名称 创建的
  props: {},
  data(){
    return{
      str:"this is new vue product",
      s:"color:white;height:40px;background:black",
      count:0,
      msg:"当前页面是组件页面，项目是通过vue create 项目名称 创建的",
      li:"<li>这是一个li标签</li>",
      danger:1,
      cj:100,
      pf:[
      "成绩A",
      "成绩B",
      "成绩C",
      "成绩D",
    ],
    red:"tit",
      rotation:[
        {id:1,"name":"波仔1","img":"1.jpg"},
        {id:2,"name":"波仔2","img":"2.jpg"},
        {id:3,"name":"波仔3","img":"3.jpg"},
        {id:4,"name":"波仔4","img":"4.jpg"}
      ],
      rotationIndex:0,
      isAlert:false
    }
  },  
  methods:{
    add(){},
    changeCount(){
      this.count +=5;
    },
    changeSex(temp){
      this.danger = temp
    },
    changeImg(temp){
      if(temp == "-"){
        this.rotationIndex--;
        // 循环逻辑
        // if(this.rotationIndex<0){
        //   this.rotationIndex = this.rotation.length-1
        // }

        //走到头停止逻辑
        if(this.rotationIndex<0){
          this.rotationIndex = 0;
          this.isAlert = true
        }
      }
      if(temp == "+"){
        this.rotationIndex++;
        //循环逻辑
        // if(this.rotationIndex>this.rotation.length-1){
        //   this.rotationIndex = 0
        // }
        if(this.rotationIndex>this.rotation.length-1){
          this.rotationIndex = this.rotation.length-1;
          this.isAlert = true
        }
      }
    },
    changeImg1(temp){
      this.rotationIndex += temp;
      if(this.rotationIndex<0){
        this.rotationIndex = 0
      }
      if(this.rotationIndex>this.rotation.length-1){
        this.rotationIndex = this.rotation.length-1
      }
    },  
    alertHide(){
      var that = this
      setTimeout(function(){
        that.isAlert = false;
      },1200)
    }
  }
}
</script>
<!-- vue脚手架创建 -->
<!-- vue create项目  vue/cli vue.js -->

<!-- 手动创建 -->
<!-- 创建html页面 引包 创建vue对象 挂载项目 定义数据 渲染数据 -->

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
