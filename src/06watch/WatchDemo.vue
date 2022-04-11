<template>
	<h3>当前求和为：{{sum}}</h3>
	<button @click="sum++">点我+1</button>
	<h3>当前信息为：{{msg}}</h3>
	<button @click="msg+='!'">修改信息</button>
	<h3>个人信息</h3>
	<h2>姓名：{{person1.name}}</h2>
	<h2>年龄：{{person1.age}}</h2>
	<button @click="person1.name+='~'">修改姓名</button>
	<button @click="person1.age++">修改年龄</button>
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

		// 情况一：监听ref所定义的单个响应式数据
		/* vue3的watch使用，watch此时是一个方法（可接收三个参数，1.要监听的属性，2.回调，3.配置项） */
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

		// 推荐写法，用数组包裹,此时newValue和oldValue的值为数组
		watch([sum, msg], (newValue, oldValue) => {
			console.log('sum或msg改变了', newValue, oldValue)
		}, { immediate: true })

		/* 情况三：监听reactive所定义的响应式对象数据
			 问题：1、此处无法正确获取oldValue
						2、强制开启了深度监视（deep配置无效）
						3、特殊情况，如果监听的是reactive定义的对象中的属性
						（例如obj:{a:{b:0}}，监听obj.a），此时deep配置有效

			监听对象时，newValue和oldValue的值为数组
		*/
		let person = reactive({
			name: '张三',
			age: 18
		})

		/* 	watch(person, (newValue, oldValue) => {
				console.log('person改变了', newValue, oldValue) // 此处无法正确获取oldValue
			}) */

		// 情况四：监听reactive定义的对象的某个属性
		// 不能直接写person.age,要写成函数的形式
		/* watch(() => person.age, (newValue, oldValue) => {
			console.log('person的age改变了', newValue, oldValue)
		}) */

		// 情况五：监听reactive定义的对象的多个属性，用数组包裹
		/* watch([() => person.name, () => person.age], (newValue, oldValue) => {
			console.log('person的name或age改变了', newValue, oldValue)
		}) */


		// 用ref定义响应式数据
		let person1 = ref({
			name: '张三',
			age: 18
		})
		// 要开启deep才能触发
		/* watch(person1, (newValue, oldValue) => {
			console.log('person1', newValue, oldValue)
		}, { deep: true })*/

		// 或对象加value属性(person1.value是ref借助reactive生成的proxy对象--value:{name:'张三',age:18})
		watch(person1.value, (newValue, oldValue) => {
			console.log('person1', newValue, oldValue)
		})



		// 返回一个对象
		return {
			sum, msg, person, person1
		}
	}
}
</script>