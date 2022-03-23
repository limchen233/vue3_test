<template>
	<h2>我是Ref组件</h2>
	<h3>个人信息</h3>
	<div>姓名：{{name}}</div>
	<div>年龄：{{age}}</div>
	<button @click="update">修改信息</button>
</template>
<script>
import { ref } from 'vue'
export default {
	name: 'RefFunction',
	setup() {
		/* 不是响应式 */
		// let name = '张三'
		// let age = 18

		let name = ref('张三')
		let age = ref(18)

		function update() {
			// name = '李四'
			// age = 20

			/* 使用ref包裹后就变成响应式数据了，但是赋值时要使用value属性 */
			name.value = '李四'
			age.value = 20
			console.log(name, age)
		}
		return {
			name,
			age,
			update
		}
	}
}
</script>