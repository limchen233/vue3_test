<template>
	<div class="son">
		<h3>我是孙组件</h3>
		<div>
			{{name}}--{{price}}
		</div>
	</div>
</template>
<script>
import { inject, toRefs } from '@vue/runtime-core'
export default {
	name: 'Son',
	setup() {
		let car = inject('car')
		return {
			...toRefs(car)
		}
	},
}
</script>
<style>
.son {
	width: auto;
	height: auto;
	background: rgb(127, 120, 231);
}
</style>