<template>
  <div class="test-container">
    <h3 id="myh3">Test.vue 组件  --- {{ books.length }}本图书</h3>
    <p id="pppp">message的值是： {{ message }}</p>
    <button @click=" message += '~'">修改message的值</button>
  </div>
</template>

<script>
export default {
    props: ['info'],
    data() {
        return {
            message: 'hello vue.js',
            //定义books数组，存储的是所有图书的列表数据。默认为空数组！
            books: []
        }
    },
    methods: {
        show() {
            console.log('调用了Test 组件的show方法！');
        },
        //使用ajax请求图书列表的数据
        initBookList() {
            const xhr = new XMLHttpRequest();
            xhr.addEventListener('load',()=> {
                const result = JSON.parse(xhr.responseText);
                console.log(result);
                this.books = result.data;
            });
            xhr.open('GET','http://www.liulongbin.top:3006/api/getbooks');
            xhr.send();
        }
    },
    //创建阶段的第一个生命周期函数
    beforeCreate() {
        // console.log(this.info);
        // console.log(this.message);
        // this.show();
    },
    created() {
        //通常在此阶段发起ajax请求拿数据
        //created生命周期函数，非常常用
        //经常在它里面，调用methods中的方法，请求服务器的数据。
        //并且，把请求到的数据，转存到data中，供template模板渲染的时候使用！
        //但是组件的模板结构尚未生成 无法操作dom
        // console.log(this.info);
        // console.log(this.message);
        // this.show();
        this.initBookList();
    },
    beforeMount() {
        //将要把内存中编译好的html结构渲染到浏览器中。此时浏览器中还没有当前组件的DOM结构
        // console.log('beforemount');
        // const dom = document.querySelector('#myh3');
        // console.log(dom);
        // console.log(this.$el);//undefined
    },
    mounted(){
        //如果要操作当前组件的DOM，最早，只能在mounted阶段执行
        // console.log(this.$el);
        // const dom = document.querySelector('#myh3');
        // console.log(dom);
    },
    beforeUpdate() {
        //将要根据变化过后、最新的数据，重新渲染组件的模板结构
        // console.log('beforeUpdate');
        // console.log(this.message);
        // const pppp = document.querySelector('#pppp');
        // console.log(pppp.innerHTML);
    },
    //当数据变化之后，为了能够操作到最新的DOM结构，必须把代码写到updated生命周期函数中
    updated() {
        console.log('Update');
        console.log(this.message);
        const pppp = document.querySelector('#pppp');
        console.log(pppp.innerHTML);
    },
    beforeDestroy() {
        //将要销毁此组件，此时尚未销毁，组件还处于正常工作状态
        console.log('beforeDestroy');
    },
    destroyed() {
        //组件已经被销毁，此组件在浏览器中对应的DOM结构已经被完全移除！
    }

}
</script>

<style lang="less" scoped>
.test-container {
    background: pink;
    height: 200px;
}
</style>