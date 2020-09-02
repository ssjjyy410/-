<template>
	<view class="input_bottom">
		<input class="input" placeholder="文明发言" placeholder-class="inputbg" type="text" v-model="text" />
		<view class="icon iconfont icon-fabu" @click="tapFabu"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				text: "",// 关键字
			};
		},
		methods:{
			//发送信息
			tapFabu(){
				this.$emit("tapFabu",this.text);
				this.text="";//清空输入框
			}
		}
	}
</script>

<style lang="less" scoped>
	.input_bottom{
		box-sizing: border-box;
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
		background-color: #fff;
		display: flex;
		align-items: center;
		padding: 15rpx 20rpx;
		border-top: 2rpx solid hsla(0,0%,0%,.1);
		z-index: 999;
		.input{
			flex: 1;
			padding: 15rpx 20rpx;
			border-radius: 10rpx;
			background-color: #f4f4f4;
			.inputbg{
				color: #8a8a8a;
			}
		}
		.icon-fabu{
			text-align: center;
			margin: 0 5rpx 0 20rpx;
			font-size: 40rpx;
		}
	}
</style>
