<template>
	<div class="child">
		<h3>我是子组件</h3>
		<div>
			{{car.name}} -- {{car.price}}
		</div>
		<Son></Son>
	</div>
</template>
<script>
import { inject } from '@vue/runtime-core'
import Son from './Son.vue'
export default {
	name: 'Child',
	components: { Son },
	setup() {
		let car = inject('car')
		return {
			car
		}
	},
}
</script>
<style>
.child {
	width: auto;
	height: auto;
	padding: 10px;
	margin: 0 auto;
	background: rgb(142, 187, 216);
}
</style>