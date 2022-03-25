<template>
	<div>
		<div>{{msg}}</div>
		<div @click="testEmit">{{name}}</div>
	</div>
</template>
<script>
export default {
	name: 'SetupDemo',
	props: ['msg', 'name'],
	beforeCreate() {
		console.log('---beforeCreate')
	},
	/* setup() {
		console.log('---setup')
		console.log(this)
	}, */

	setup(props, context) { // props要先在上面声明才能接收到值
		console.log(props) // Proxy{msg:'hello',name:'张三'}
		console.log(context) // 包含emit方法

		function testEmit() {
			context.emit('hello', 666) // 子组件触发父组件事件
		}

		return {
			testEmit
		}
	}

	/* 注意：
		1、setup早于beforeCreate执行
		2、setup中this是undefined
		3、setup接收两个参数，默认是props和context；
			 props要先声明才能接收到值，值是Proxy对象。
			 context：上下文对象
					attrs：值为对象相当于this.$attrs
					slots：收到的插槽内容，相当于this.$slots
					emit：分发自定义事件的函数，相当于this.$emit
	
	
	*/
}
</script>
