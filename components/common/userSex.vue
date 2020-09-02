<template>
	<view :class="`usersex ${sex===1?'colorNv':''}`">
		<view :class="`icon iconfont ${sex===0?'icon-nan':'icon-nv'}`"></view>{{age}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:["sex","age"]
	}
</script>

<style lang="less">
	.usersex{
		display: inline-block;
		font-size: 30rpx;
		padding: 2rpx 10rpx;
		color: #fff;
		background-color: #44b3ff;
		border-radius: 30rpx;
		.icon{
			display: inline-block;
			margin-right: 5rpx;
		}
	}
	.colorNv{
		background-color: #ff6b8d !important;
	}
</style>
