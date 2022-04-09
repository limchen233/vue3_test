<template>
	<h3>当前求和为：{{sum}}</h3>
	<button @click="sum++">点我+1</button>
	<h3>当前信息为：{{msg}}</h3>
	<button @click="msg+='!'">修改信息</button>
	<h3>个人信息</h3>
	<h2>姓名：{{person.name}}</h2>
	<h2>年龄：{{person.age}}</h2>
	<button @click="person.name+='~'">修改姓名</button>
	<button @click="person.age++">修改年龄</button>
</template>
<script>
import { reactive, ref } from '@vue/reactivity'
import { watch } from '@vue/runtime-core'
export default {
	name: 'WatchDemo',
	// vue2方式
	/* watch: {
		sum(newValue, oldValue) {
			console.log('sum改变了', newValue, oldValue);
		}
	}, */
	setup() {
		// 数据
		let sum = ref(0)


		/* vue3的watch使用，watch此时是一个方法（可接收三个参数，1.要监听的属性，2.回调，3.配置项） */
		// 情况一：监听ref所定义的单个响应式数据
		watch(sum, (newValue, oldValue) => {
			console.log('sum改变了', newValue, oldValue)
		})

		// 情况二：监听ref所定义的多个响应式数据
		let msg = ref('你好')
		// vue3中可写多个watch,普通写法
		/* watch(sum, (newValue, oldValue) => {
			console.log('sum改变了', newValue, oldValue)
		})
		watch(msg, (newValue, oldValue) => {
			console.log('msg改变了', newValue, oldValue)
		}) */

		// 推荐写法
		watch([sum, msg], (newValue, oldValue) => {
			console.log('sum或msg改变了', newValue, oldValue)
		}, { immediate: true })

		// 情况三：监听ref所定义的多个响应式数据
		let person = reactive({
			name: '张三',
			age: 18
		})

		watch(person, (newValue, oldValue) => {
			console.log('person改变了', newValue, oldValue) // 此处无法正确获取oldValue
		})








		// 返回一个对象
		return {
			sum, msg, person
		}
	}
}
</script>