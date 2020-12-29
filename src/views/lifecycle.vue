<template>
  <div class="lifecycle">
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      foo:"foo"
    };
  },
  beforeCreate() {
    //组件实例还未创建，通常用于插件开发中执行一些初始化任务（数据校验等）
    console.log("beforeCreate")
  },
  created(){
    //组件初始化完毕，各种数据可以使用，常用于异步数据获取
    console.log('created => ' + this.$el)
  },
  beforeMounted() {
    // 虚拟dom(vm.$el)转换为真实dom(el) DOM转换还未完成，还未创建
    console.log('beforeMount')
  },
  mounted() {
    //初始化结束，虚拟dom转换真实dom已完成 可访问dom元素
    setTimeout(()=>{
      this.foo = 'foooooo'
    },2000)
    console.log('mounted',this.$el)
  },
  beforeUpdate() {
    // 更新前，可以用于获取更新各种状态 => 滚动条位置
    console.log('beforeUpdate')
  },
  updated() {
    //更新后，所有状态已是最新
    console.log('updated')
  },
  beforeDestroy() {
    //销毁前，可用于一些定时器或订阅的取消
  },
  destroyed() {
    //组件已经销毁，作用同上
  },
};
</script>

<style lang="scss" scoped>

</style>
