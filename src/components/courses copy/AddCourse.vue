<template>
  <div>
    <p>
      <input type="text" :value="value" @input="onInput" v-on:keydown.enter="courseAdd" ref="addipt" />
      <button @click="courseAdd">新增</button>
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // course: "",
    }
  },
  props: {
    value: {
      type: String,
      default: ''
    },
  },
  mounted () {
    this.$refs.addipt.focus();
  },
  methods: {
    courseAdd() {
      //羊肉串命名  驼峰命名--父组件可能监听不到
      this.$emit('course-add')
      
    },
    onInput(e){
      this.$emit('input',e.target.value)
    }
  },
};
</script>

<style lang="scss" scoped></style>
