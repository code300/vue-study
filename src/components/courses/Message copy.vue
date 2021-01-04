<template>
  <div>
    <transition name="fade">
      <div class="message-box" v-if="show">
        <!-- 作用域插槽（可从子组件获取内容） -->
        <!-- <slot name="title" title="作用域插槽">默认内容</slot> -->
        <!-- 具名插槽-获取指定内容的插槽（没有指定内容会使用默认内容） -->
        <slot name="title">默认内容</slot>
        <!-- 通过slot获取插槽内容 -->
        <slot></slot>
        <!-- 自定义事件处理必须为update:show -->
        <span class="message-box-close" @click="toggle">X</span>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
    };
  },
  props: {
    msg: {
      type: String,
      default: "",
    },
  },
  mounted() {
    this.$bus.$on("message-close", () => {
      this.toggle();
    });
  },
  methods: {
    toggle() {
      this.show = !this.show;
    },
  },
};
</script>

<style lang="scss" scoped>
.message-box {
  // background-color: cadetblue;

  margin: 0 auto;
}
.success {
  background: #4fc08d;
}
.warning {
  background: #f66;
}
.fade-enter,.fade-leave-to{
  opacity: 0;
}
.fade-enter-active,.fade-leave-active{
  transition: opacity 1.5s;
}
</style>