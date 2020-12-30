<template>
  <div>
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: "",
    };
  },
  mounted() {
    console.log(this.courses, "666");
  },
  props: {
    courses: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
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
