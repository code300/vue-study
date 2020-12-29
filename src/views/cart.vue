<template>
  <div class="test1">
    <!-- 输入框--双向绑定 -->

    <p>
      <input type="text" v-model="course" v-on:keydown.enter="addCourse" />
      <button @click="addCourse">新增</button>
    </p>

    <!-- 条件渲染 -->
    <p v-if="courses.length == 0">没有任何课程信息</p>

    <!-- 遍历-列表渲染--选中状态 -->
    <!-- <div v-for="item in courses" :key="item" :class="{active:selected === item}" @click="selected = item">
      {{ item }}
    </div> -->
    <ul class="course-list" v-else>
      <li
        v-for="item in courses"
        :key="item"
        :style="{ backgroundColor: selected === item ? '#ddd' : '' }"
        @click="selected = item"
      >
        {{ item }}
      </li>
    </ul>

    <p>课程总数：{{ totalCount }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      course: "",
      courses: [],
      selected: "",
      totalCount: 0,
    };
  },
  async created(){
    //组件实例已经创建,由于未挂载，dom不存在
    this.courses = await this.getCourses()
  },
  mounted(){
    //vue模板已经通过render函数转换为虚拟dom，已经可以访问dom了
  },
  methods: {
    addCourse() {
      // 1.添加 course到数组
      this.courses.push(this.course);
      // 2.清空数组
      this.course = "";
    },
    render() {
      // console.log(this.$options.render,'render')
      // 编写的vue模板 => 会转换成render渲染函数 => 虚拟DOM =>真实dom
    },
    // 模拟异步数据调用
    getCourses(){
      return new Promise(resolve => {
        setTimeout(()=>{
          resolve(["web", "web2"]) 
        },2000)
      })
    }
  },
  computed: {
    total() {
      //   计算属性是有缓存性：如果值没有变化，则页面不会重新渲染
      return this.courses.length + "门";
    },
  },
  //   默认情况下watch初始化时不执行，有变化后才执行
//   watch: {
//     courses(newVal) {
//       this.totalCount = newVal.length + "门";
//     },
//   },
//   默认情况下watch初始化时会立即执行
  watch: {
    courses: {
      immediate: true,//立即执行
      deep: true, //针对数据深层次监听 例如数组对象中的值（消耗会很大）
      handler(newValue, oldValue) {
          this.totalCount = newValue.length + "门";
          console.log(oldValue)
      },
    },
  },
  // 模拟异步数据调用

};
</script>

<style lang="scss" scoped>
.active {
  background-color: #ddd;
}
li {
  list-style: none;
}
</style>
