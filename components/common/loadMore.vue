<template>
	<view class="load_more">
		{{loadContext}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["loadContext"]
	}
</script>

<style lang="less" scoped>
	.load_more{
		line-height: 100rpx;
		text-align: center;
		font-size: 30rpx;
		color: #bbb;
	}
</style>
