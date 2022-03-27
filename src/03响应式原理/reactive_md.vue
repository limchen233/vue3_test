<template>
	<div>
		<h2>个人信息</h2>
		<h3>姓名：{{person.name}}</h3>
		<h3 v-show="person.age">年龄：{{person.age}}</h3>
		<button @click="addInfo">添加个人信息</button>
	</div>
</template>
<script>
import { reactive } from '@vue/reactivity'
export default {
	setup() {
		let person = reactive({
			name: '张三'
		})

		function addInfo() {
			person.age = 20
		}

		return {
			person,
			addInfo
		}
	},
}
</script>