<template>
  <div>
    <h5>Count 组件</h5>
    <p>count的值是: {{ count }}</p>
    <!-- 下面是错误做法 会终端报错 -->
    <button @click="count += 1">+1</button>
    <button @click="show">打印this</button>
  </div>
</template>

<script>
export default {
  //props是“自定义属性”，允许使用者通过自定义属性，为当前组件指定初始值
  //自定义属性的名字，是封装者自定义的(只要名称合法即可)
  //props中的数据，可以直接在模板结构中被使用
  // props: ['init'],
  props: {
    //自定义属性A:{/* 配置选项 */},
    //自定义属性B:{/* 配置选项 */},
    //自定义属性C:{/* 配置选项 */},
    init: {
      default: 0,
      type: Number,
      required: true
    }
  },
  data() {
    return {
      count: this.init
    }
  },
  methods: {
    show() {
      console.log(this);
    }
  }
  // methods: {
  //   add() {
  //     this.count += 1;
  //   }
  // }
}
</script>

<style lang="less">

</style>