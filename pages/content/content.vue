<template>
	<view>
		上一页内容：{{content}} id:{{id}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				content:"buk",
				id:"1"
			};
		},
		onLoad:function(op){
			this.content = op.name
		}
	}
</script>

<style lang="stylus">

</style>
