<template>
  <div class="page1">
      <!-- ///  出现这种情况是因为依赖路由的params参数获取写在created生命周期里面,
      因为路由懒加载的关系，退出页面再进入另一个文章页面并不会运行created组件生命周期,
      导致文章数据还是第一次进入的1      /// -->
    <button @click="changeMessage">改变message</button>          
    <button @click="toPageTwo"></button> 

  </div>
</template>
<script>
  export default {
    data(){
      return{
         message:'路由传递过来的值',   // 数据是第一次进来和第二进来是不变化的 
      }
    },
      //   比方说前面路由叫page.vue  路由传值  举个例子传递了  100
      //   ==============           this.$router.push({path:'/page1',query:{msg:this.list}});
    created() {
      this.message = this.$route.query.msg
      console.log(this.message)   //第一次和接下来都会输出100
    },
    ///////////////////////////////
    //////////////////////////
    ///////////////////
   /// 解决方案////////
   //////////////////
   //////////////////////////////  watch监听路由变化来改变值  
    watch:function(){
      '$route'(to, from) {
        if (to.path == "/page") {    /// 路由名看你跳转前的路由名字决定  
           this.message = this.$route.query.msg        //这样当page.vue中值发生变化  也会传递过来 刷新page1的值   
        }
      }
    },
    methods:{
      ...
       
       ...
    },

  }
</script>

<style scoped>
  
</style>
