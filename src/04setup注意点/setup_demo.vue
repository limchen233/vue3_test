<template>
	<div></div>
</template>
<script>
export default {
	name: 'SetupDemo',
	beforeCreate() {
		console.log('---beforeCreate')
	},
	setup() {
		console.log('---setup')
		console.log(this)
	},

	/* 注意：
		1、setup早于beforeCreate执行
		2、setup中this是undefined
	
	
	*/
}
</script>
