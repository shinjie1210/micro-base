<template>
    <div>
        <img alt="Vue logo" src="./assets/logo.png" />
    </div>
    <p>基座应用</p>
    <button @click="toFoo">to foo</button>
    <button @click="toBar">to bar</button>
    <button @click="toSon">to son</button>
    <router-view></router-view>

</template>
<script setup>
import {
    useRouter
} from 'vue-router' //引入router
import {
    useStore
} from 'vuex' //引入vuex
import { //引入生命周期函数--------------------添加内容
    onMounted
} from 'vue';
import { //引入定义的请求--------------------添加内容
    userLogin
} from './api/index'
const router = useRouter()
const store = useStore()
//发请求--------------------添加内容
onMounted(() => {
    userLogin({
        //你的请求字段
    }).then(res => {
        console.log(res);
    }).catch(error => {
        console.log(error);
    })
})
//路由跳转测试
function toFoo() {
    router.push({
        path: '/foo'
    })
}

function toBar() {
    router.push({
        path: '/bar'
    })
}
const toSon = () => {
    router.push({
        path: '/son'
    })
}

//修改数据func测试
function addState() {
    store.commit('add')
}

function minState() {
    store.commit('min')
}
//异步func测试
function changeState() {
    store.dispatch('change', 99)
}
</script>

<style>
#app {
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>