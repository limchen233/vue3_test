<template>
	<h2>我是Reactive组件</h2>
	<h3>个人信息</h3>
	<div>姓名：{{person.name}}</div>
	<div>年龄：{{person.age}}</div>
	<div>地址：{{person.addr}}</div>
	<div>爱好：{{person.hobby}}</div>
	<button @click="update">修改信息</button>
</template>
<script>
import { reactive } from 'vue'
export default {
	name: 'RefFunction',
	setup() {

		// let name = ref('张三')
		// let age = ref(18)

		// 对象时使用reactive
		/* let job = reactive({
			job_name: '前端开发',
			dept: '数字化运营中心',
			addr: '南京',
			hobby: ['学习', '音乐']
		}) */

		/* 统一使用reactive函数 */
		let person = reactive({
			name: 'hello',
			age: 20,
			addr: '南京',
			hobby: ['学习', '音乐']
		})

		function update() {
			/* 使用ref包裹后就变成响应式数据了，但是基本数据赋值时要使用value属性 */
			// name.value = '李四'
			// age.value = 20

			person.name = '张三'

			// 引用类型（ref函数借助了reactive函数）
			// job.job_name = 'UI设计师'
			// job.addr = '上海'

			// 数组可通过下标直接修改
			// job.hobby[0] = '电影'

			person.hobby[0] = '电影'

		}
		return {
			// name,
			// age,
			// update,
			// job
			person,
			update
		}
	}

	/* 总结
		reactive函数：
		1、定义一个对象类型的响应式数据 const 代理对象 = reactive(源对象)，返回一个代理对象（Proxy的实例对象）
		2、reactive定义的响应式数据是深层次的
	*/
}
</script>