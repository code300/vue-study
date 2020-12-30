<template>
  <div class="cart">
    <Message :show.sync="show">
      <!-- 作用域插槽 -->
      <!-- <template v-slot:title="slotProps">
        <strong>{{slotProps.title}}</strong>
      </template> -->
       <!-- 具名插槽 -->
      <template v-slot:title>
        <strong>{{title}}</strong>
      </template>
      <!-- 默认插槽 -->
      <template v-slot:default>
          {{msg}}
      </template>
    </Message>
    <!-- 输入框--自定义事件双向绑定（增加组件可复用性） -->
    <AddCourse v-model="course" @course-add="courseAdd" />
   <!-- <AddCourse :value="course" @input="course=$event" @course-add="courseAdd" /> -->

    <CoursesList :courses="courses"  />
    <p>课程总数：{{ totalCount }}</p>
  </div>
</template>

<script>
import CoursesList from "@/components/courses/Courses";
import AddCourse from "@/components/courses/AddCourse";
import Message from "@/components/courses/Message"
export default {
  data() {
    return {
      title:'go!',
      courses: [],
      course:'',
      totalCount: 0,
      show:false,
      msg:'新增成功!'
    };
  },
  components: {
    CoursesList,
    AddCourse,
    Message
  },
  async created(){
    //组件实例已经创建,由于未挂载，dom不存在
    this.courses = await this.getCourses()
  },
  mounted(){
    //vue模板已经通过render函数转换为虚拟dom，已经可以访问dom了
  },
  methods: {
    courseAdd() {
      // 1.添加 course到数组
      this.courses.push(this.course);
      // 2.清空数组
      this.course = "";
      this.show = true
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

</style>
