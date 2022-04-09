<template>
	<h3>当前求和为：{{sum}}</h3>
	<button @click="sum++">点我+1</button>
	<h3>当前信息为：{{msg}}</h3>
	<button @click="msg+='!'">修改信息</button>
	<h3>个人信息</h3>
	<h2>姓名：{{person.name}}</h2>
	<h2>年龄：{{person.age}}</h2>
	<h3>薪资：{{person.job.a.salary}}</h3>
	<button @click="person.name+='~'">修改姓名</button>
	<button @click="person.age++">修改年龄</button>
	<button @click="person.job.a.salary++">涨薪</button>
</template>
<script>
import { reactive, ref, watch, watchEffect } from 'vue'
export default ({
	setup() {
		// 数据
		let sum = ref(0)
		let msg = ref('你好')
		let person = reactive({
			name: '张三',
			age: 18,
			job: {
				a: {
					salary: 20
				}
			}
		})

		// 监听
		watch(sum, (newValue, oldValue) => {
			console.log('sum改变了', newValue, oldValue);
		})

		/* 
			watchEffect不用指定监听哪个属性，监听回调中用到哪个属性，就监听哪个属性
		*/
		watchEffect(() => {
			const a = sum.value
			const b = person.job.a.salary
			console.log('watchEffect所指定的回调执行了', a, b);
		})

		return {
			sum, msg, person
		}
	},
})
</script>
