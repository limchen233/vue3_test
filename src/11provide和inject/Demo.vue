<template>
	<div class="app">
		<h3>我是祖先组件</h3>
		<div>{{name}}--{{price}}</div>
		<Child></Child>
	</div>
</template>
<script>
import Child from './Child.vue'
import { reactive, toRefs } from '@vue/reactivity'
import { provide } from '@vue/runtime-core'
export default {
	name: 'PIDemo',
	components: { Child },
	setup() {
		let car = reactive({ name: '奔驰', price: '50W' })
		provide('car', car) // 给后代组件提供数据
		return {
			...toRefs(car)
		}
	},
}
</script>
<style>
.app {
	width: 50%;
	height: 300px;
	background: gray;
	padding: 10px;
	margin: 0 auto;
	overflow: hidden;
}
h3 {
	margin: 5px;
}
</style>