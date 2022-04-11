<template>
	<h3>个人信息</h3>
	<!-- <h2>姓名：{{person.name}}</h2>
	<h2>年龄：{{person.age}}</h2>
	<h3>薪资：{{person.job.a.salary}}</h3>
	<button @click="person.name+='~'">修改姓名</button>
	<button @click="person.age++">修改年龄</button>
	<button @click="person.job.a.salary++">涨薪</button> -->

	<!-- 用对象点属性很麻烦，直接使用变量名 -->
	<h2>姓名：{{name}}</h2>
	<h2>年龄：{{age}}</h2>
	<h3>薪资：{{job.a.salary}}</h3>
	<button @click="name+='~'">修改姓名</button>
	<button @click="age++">修改年龄</button>
	<button @click="job.a.salary++">涨薪</button>
</template>
<script>
import { toRefs, reactive } from 'vue'
export default ({
	setup() {
		// 数据
		let person = reactive({
			name: '张三',
			age: 18,
			job: {
				a: {
					salary: 20
				}
			}
		})

		// 返回一个对象（常用）
		/* return {
			person
		} */

		// 这种写法可正常展示，但丢失了响应式（因为person.name现在只是一个字符串）
		/* return {
			name: person.name,
			age: person.age,
			salary: person.job.a.salary
		} */

		// 使用ref,可正常响应，但原数据不会改变。因为改变的是用ref新创建的那个对象。
		/* return {
			name: ref(person.name), // 新创建了一个ref对象
			age: ref(person.age),
			salary: ref(person.job.a.salary)
		} */

		// 使用toRef，处理单个ref对象
		/* return {
			name: toRef(person, 'name'),
			age: toRef(person, 'age'),
			salary: toRef(person.job.a, 'salary')
		} */

		// 使用toRefs,处理多个ref对象
		const a = toRefs(person)
		console.log(a) // 此时a是一个响应式对象{name:'',age:'',...}
		return {
			...toRefs(person) // 只能取对象的第一层属性，嵌套的属性salary还是要单独写
		}
	},
})
</script>
