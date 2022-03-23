<template>
	<h2>我是App组件</h2>
	<h3>个人信息</h3>
	<div>姓名：{{name}}</div>
	<div>年龄{{age}}</div>
	<button @click="say">说话</button>
	<hr>
	<RefFunction></RefFunction>
	<hr>
	<TestReactive></TestReactive>
</template>

<script>
// import { h } from '@vue/runtime-core'
import RefFunction from './02ref/ref_function.vue'
import TestReactive from './02ref/test_reactive.vue'

export default {
	name: 'App',
	components: {
		RefFunction, TestReactive
	},
	/* 测试setup函数，不考虑响应式 */
	setup() {
		/* 数据 */
		let name = '张三'
		let age = 18

		/* 方法 */
		function say() {
			alert(`大家好，我是${name},今年${age}岁了`)
		}

		/* return一个对象（常用） */
		return {
			name,
			age,
			say
		}

		// return一个渲染函数
		// return () => h('h1', 'HelloWorld')
	}

	/* 注意点 */
	// 1、尽量还要与vue2配置混用
	//  1.1 vue2配置（data，methods，computed）中可以访问到setup中的属性、方法
	//  1.2 setup中不能访问到vue2的配置
	//  1.3 属性如果有重名，setup优先
	// 2、setup不能是一个async函数，因为返回值不再是return的对象，而是promise，模板看不到return对象中的属性
}
</script>


<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
