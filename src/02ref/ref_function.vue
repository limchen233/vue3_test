<template>
	<h2>我是Ref组件</h2>
	<h3>个人信息</h3>
	<div>姓名：{{name}}</div>
	<div>年龄：{{age}}</div>
	<div>职位：{{job.job_name}}</div>
	<div>部门：{{job.dept}}</div>
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

		let job = ref({
			job_name: '前端开发',
			dept: '数字化运营中心'
		})

		function update() {
			// name = '李四'
			// age = 20

			/* 使用ref包裹后就变成响应式数据了，但是基本数据赋值时要使用value属性 */
			name.value = '李四'
			age.value = 20
			console.log(name, age)

			// 引用类型
			job.value.job_name = 'UI设计师'
			console.log(job.value)
		}
		return {
			name,
			age,
			update,
			job
		}
	}

	/* 总结
		ref函数：
		1、定义一个响应式数据 const name = ref(xxx)
		2、接收的数据可以是基本数据类型，也可以是对象类型
		3、基本数据类型：响应式依然是靠Object.defineProperty()的get与set完成的
		4、对象数据类型使用了Proxy代理（reactive函数）
	
	*/
}
</script>