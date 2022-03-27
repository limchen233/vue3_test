<template>
	<h1>测试计算属性</h1>
	姓：<input type="text" v-model="person.firstname">
	<br>
	名：<input type="text" v-model="person.lastname">
	<br>
	<span>全名：{{person.fullname}}</span>
</template>
<script>
import { reactive, computed } from 'vue'
export default {
	name: 'ComputedDemo',
	setup() {
		// 定义数据
		let person = reactive({
			firstname: '张',
			lastname: '三'
		})

		// 计算属性
		// let fullname = computed(() => {
		// 	return person.firstname + person.lastname
		// })

		// 直接在对象上追加属性
		person.fullname = computed(() => {
			return person.firstname + person.lastname
		})

		// 返回数据
		return {
			person,
			// fullname
		}

	}
}
</script>